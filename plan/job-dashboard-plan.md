# Plan: private job dashboard and Monday launch (26 Nov 2026)

Goal: by Sun 30 Nov everything is ready, so from Mon 1 Dec Ayush can start sending applications.
Status: research and plan only. Nothing is built yet. No job gets an application or mail without Ayush saying yes for that job.

This plan reuses what is already in this repo:
- Profile: [profile/ayush-profile.md](../profile/ayush-profile.md)
- Jobs found so far + cover note drafts: [jobs/shortlist.md](../jobs/shortlist.md)
- Interview data per company: [jobs/companies/](../jobs/companies/README.md)
- Interview patterns from 35+ other candidates: [research/other-candidates-2026.md](../research/other-candidates-2026.md)
- Interview prep by company type: [research/interview-prep-2026.md](../research/interview-prep-2026.md)
- Market and salary: [market/market-report-2026-11.md](../market/market-report-2026-11.md)
- Learning plan (JobMatch AI project): [learning/README.md](../learning/README.md)

Raw notes and sources for this plan: [research/raw/2026-11-26-dashboard-sources.md](../research/raw/2026-11-26-dashboard-sources.md)

---

## 0. The big idea in one paragraph

The dashboard is a private page inside the portfolio (ayushpathak.co.in, repo common-portfolio, Next.js 16 on Vercel). Only Ayush can log in, with one fixed user id and password. Each job is one card. Every card holds: the job details, a priority score, a chance-of-selection estimate with reasons, a mock interview set, a tailored resume, a cover note, and the status (saved, applied, interview, offer, rejected). Claude does the thinking work (scoring, mocks, resume changes) in this project and puts the results into the dashboard. Ayush reviews and decides what to send.

Bonus: this dashboard is the same app idea as "JobMatch AI" from the 12-day learning plan. So building it is also the learning project and a strong interview story.

---

## 1. Private login with one fixed user id and password

### What we will do

Keep it small. No sign-up, no database of users, no third party login.

1. **Secrets live only in Vercel environment variables**, never in the code or Git:
   - `DASH_USER` : the user id
   - `DASH_PASS_HASH` : a hash of the password (not the password itself). Use Node's built-in `crypto.scrypt`, so no extra package.
   - `DASH_SESSION_SECRET` : a long random string (32+ bytes) used to sign the login cookie.
2. **Login page** at a plain route such as `/dashboard/login`. The form posts to a Server Action.
3. **The Server Action checks the login**:
   - Rate limit first: 5 tries per 15 minutes per IP, using the Upstash Redis rate limiter the portfolio already uses for the AI chat.
   - Compare user id and password hash with `crypto.timingSafeEqual` (so time taken does not leak anything).
   - Same error message for wrong id and wrong password.
4. **On success, set one cookie** with a signed token (JWT made with the `jose` library, HS256, signed with `DASH_SESSION_SECRET`). Cookie settings: `httpOnly`, `secure`, `sameSite: 'strict'`, `path: '/'`, expires in 7 days. Never store the token in localStorage.
5. **Check the login in two places**:
   - `proxy.ts` (Next.js 16 name for middleware): quick check, redirect to login if no valid cookie. This is only a first gate.
   - A small `requireAdmin()` helper that every dashboard page, Server Action and API route calls before it reads or writes any job data. This is the real lock.
   - Why both: in 2025 there was a Next.js bug (CVE-2025-29927) where a special header let people skip middleware completely. Apps that checked only in middleware were open. Checking again near the data protects us even if the first gate fails. Also keep Next.js on the latest patch.
6. **Keep the page hidden from search engines**: `robots: { index: false }` on the dashboard layout, `Disallow: /dashboard` in robots.txt, and no link to it from the public site.
7. **Logout** button clears the cookie. To log out from everywhere, just change `DASH_SESSION_SECRET` in Vercel and redeploy.
8. **Job data never goes into the public bundle** (no JSON in `/public`, no data imported into client components without the auth check).

Later, if wanted: a 6-digit authenticator app code (TOTP) as a second step. Not needed for the weekend.

### Other options we looked at

| Option | Why not first choice |
|---|---|
| Auth.js v5 Credentials provider | Ayush already used it at FITPASS, so it is a fine choice. But for one fixed user it adds more setup than ~40 lines with `jose`. Pick this if Ayush prefers it. |
| Vercel password protection | Works at deployment level, but is a paid add-on and protects whole deployments, not one route. |
| Clerk / Better Auth | Made for many users. Too much for one person. |

### Interview value

This gives a real story: "I protected a private route in Next.js 16. I did not trust middleware alone because of CVE-2025-29927, so I added a data access check." That is a senior-level answer.

---

## 2. Where to keep the job data

### Recommendation: Upstash Redis (the account the portfolio already has)

- The portfolio already uses Upstash Redis (rate limit) and Upstash Vector (AI assistant). No new account, works over REST from Vercel functions.
- Free tier: 1 database, 250 MB data, about 500K commands a month. One job with all its content is maybe 20-50 KB. Even 300 jobs is well under 15 MB.
- Free tier has no encryption at rest. That is fine for job notes. Do not store passwords, ID documents, or bank details there.
- Use a key prefix so it does not mix with rate limit keys: `jobs:item:<id>`, `jobs:index` (sorted set by score), `jobs:events:<id>` (status history).

Each job is one JSON document checked with a Zod schema:

```ts
type Job = {
  id: string;              // e.g. "conxai-senior-fe-2026-11"
  company: string;
  title: string;
  link: string;
  location: string;        // "Gurugram, office" / "Remote, US hours"
  source: string;          // Indeed, LinkedIn, referral, careers page
  postedOn?: string;
  salaryRange?: string;
  jdText: string;          // full job description, saved because posts get removed
  status: "saved" | "ready" | "applied" | "interview" | "offer" | "rejected" | "skipped";
  score: { total: number; parts: Record<string, number>; notes: string };
  chance: { shortlist: number; clear: number; overall: number; band: "low" | "medium" | "high"; reasons: string[] };
  mock?: MockInterview;     // section 4
  resume?: { markdown: string; changes: string[]; pdfUrl?: string };
  coverNote?: string;
  contacts?: { name: string; role: string; link: string }[];
  timeline: { at: string; what: string }[];
  nextStep?: { what: string; due: string };
};
```

### Other options

| Option | When to pick it |
|---|---|
| Neon or Supabase Postgres (free) | If Ayush wants this to double as Day 5 of the learning plan (Node + Postgres). Better for filters and reports. A bit more setup. |
| JSON files in a private GitHub repo | Simple and has history, but every edit is a commit and the dashboard needs a GitHub token. |
| Vercel Blob (private) | Good later for storing tailored resume PDFs. |

### How Claude puts data into the dashboard

Claude does the scoring, mocks and resume work in this project. Two ways to move it in:

1. **Weekend version (simplest):** a protected import route `POST /api/dashboard/import` that takes a job JSON. It needs its own secret header (`DASH_IMPORT_TOKEN`, different from the login). Claude sends jobs there; Ayush can turn the token off any time by deleting the env variable.
2. **Fallback:** Claude writes the JSON file, Ayush pastes it into an "Import" box on the dashboard.

### Important: this repo is public

`iayushpathak-dev/find-jobs` is public right now. Salary numbers, notice period, recruiter names and tailored resumes should not be public. Suggestion: make this repo private (GitHub > Settings > Danger zone > Change visibility). Until then, Claude will keep personal numbers out of this repo and only in the dashboard.

---

## 3. Job priority score (0 to 100)

Each job gets a score from these parts. Weights are a starting point and can change.

| Part | Max | How we score it |
|---|---|---|
| Skill match | 30 | Share of the job's must-have skills Ayush really has (React, Next.js, TS, AI features, testing...). Nice-to-haves count half. |
| Experience fit | 15 | Ask is within 5-8 yrs = full. 1-2 yrs off = half. Ask 10+ or under 3 = low. Uses total experience (~6y10m). |
| Pay fit | 15 | Listed or known band vs Ayush's minimum (need this number from Ayush). Unknown = middle score. |
| Location / hours | 10 | Delhi NCR or remote IST = full. Bengaluru hybrid / US hours = depends on Ayush's answer. |
| Growth and title | 10 | AI product work, Next.js App Router, ownership, "AI Product Engineer" type title = high. |
| Company signal | 10 | Funding/stability, good reviews, interview data we have (jobs/companies/). Low-pay reports lower it. |
| Freshness | 5 | Posted in last 7 days = full, 8-30 days = half, older = 0. |
| Way in | 5 | Referral or recruiter contact = full, cold apply = 1. |

**Hard filters (skip before scoring):** pay clearly under Ayush's floor, pure backend/ML/Python roles, listing older than 60 days with no sign it is open, US night shift if Ayush says no.

**Buckets:**
- **A (75+):** apply first, full tailoring, mock interview prepared before applying.
- **B (60-74):** apply with lighter tailoring.
- **C (under 60):** keep in list, do not spend time now.

Example using current shortlist (rough, before Ayush's salary and location answers): CONXAI about 80 (A), Mercari India about 75 (A, if Bengaluru is ok), Mirantis about 60 (B, asks 8+ yrs), Hire Hangar about 60 (B, US hours), Avya and Ken Research under 55 (C).

---

## 4. Mock interview for each job

### Input
- The job description.
- Company interview data from `jobs/companies/<company>.md` (rounds, real questions from candidates).
- General patterns from `research/other-candidates-2026.md` (for example: streaming chat UI is now a common machine coding round for frontend + AI roles).
- Ayush's real projects (portfolio case studies, later local projects from section 7).

### What Claude makes per job
1. **Expected rounds** (for example CONXAI: CEO call, then CTO + senior engineer technical).
2. **For each round, 6 to 10 questions**, mixed:
   - JS / React deep questions linked to that job's stack.
   - One machine coding task in the style that company uses (Mercari: 2 React problems on HackerRank).
   - One frontend system design question close to their product.
   - 3 behaviour questions with the STAR answer outline from Ayush's own projects.
   - 2 questions about the company's product ("how would you build X on our app").
3. **For each question:** what a strong answer must cover, a common mistake, and the follow-up the interviewer will likely ask.
4. **Questions for Ayush to ask them** (3-4).

### How a practice session works
- Ayush answers in this project (typing or voice note text). Claude plays the interviewer, asks follow-ups, then scores.
- Score each answer 1-5 on: correct, explains why (not only what), trade-offs, clear speaking, uses real examples. ("Explaining what but not why" was a top rejection reason in our candidate research.)
- Weak areas go into a short "fix list" with a 20-minute task for each.
- The mock score feeds the "clear the rounds" part of the chance estimate (section 5).

Stored as:
```ts
type MockInterview = {
  rounds: { name: string; questions: { q: string; mustCover: string[]; trap: string; followUp: string }[] }[];
  attempts: { at: string; scores: number[]; fixList: string[] }[];
};
```

---

## 5. Chance of selection (%)

### Honest warning first
There is no public data that can give a true percentage for one person and one job. ATS tools like Jobscan and scale.jobs give a match score, but they do not publish real data linking score to interview calls. So our percent is an **estimate with reasons**, not a fact. We will correct it with Ayush's real results after 20-30 applications.

### The method: split it into two steps

**Overall chance = chance of getting shortlisted x chance of clearing the rounds**

**Step A: shortlist chance**

Start with a base by how we apply, then multiply:

| Factor | Values (starting guesses, to be corrected with real results) |
|---|---|
| Base by channel | Cold apply on job board: 5%. Company careers page: 7%. Recruiter reached out: 30%. Referral: 20%. |
| Must-have skill coverage | 90%+: x2.0. 70-89%: x1.3. 50-69%: x0.7. Under 50%: x0.3 |
| Experience fit | In range: x1.0. Short by 1-2 yrs: x0.6. Way more than asked: x0.7 |
| Freshness | 0-7 days: x1.3. 8-30 days: x1.0. Older: x0.5 |
| Location fit | Same city / remote: x1.0. Needs relocation: x0.6 |

Cap at 80%.

**Step B: clear-the-rounds chance**

Based on mock interview scores for that company's rounds:
- Average mock score 4.5+ = 60%, 4.0-4.4 = 45%, 3.5-3.9 = 30%, 3.0-3.4 = 18%, under 3 = 8%.
- Minus 10 points for each round type we have no practice for yet (for example a DSA round when only React was practiced).
- Before any mock is done, use 25% as a placeholder.

**Example (CONXAI, cold apply, before mocks):** 5% x 2.0 (skills) x 1.0 (exp) x 1.0 (freshness) x 1.0 (NCR) = 10% shortlist. 10% x 25% = 2.5% overall. With a referral: 20% x 2.0 = 40% shortlist, so 10% overall. After good mocks (4.2 avg): 40% x 45% = 18%.

This also shows what moves the number most: **a referral or recruiter contact changes the chance 4 to 6 times more than resume tweaks.** So the plan spends time on finding a contact at each A-bucket company.

Each job card shows: the % numbers, the band (Low under 5%, Medium 5-15%, High over 15% overall), and 3 to 5 reasons in plain words ("Missing: Playwright. They ask 8+ years. No referral yet.").

### Calibrating later
Every status change is saved with a date. After 20-30 applications we compare our guessed shortlist % with what really happened, by channel and by bucket, and adjust the base numbers.

---

## 6. Tailored resume for each job

Waiting on: **the resume format from Ayush** (Word / Google Doc / LaTeX / Figma?).

The method once we have it:
1. **Master resume first.** One long file with every true bullet Ayush has, each with a number where possible (users, speed, time saved, clients). Built from the portfolio, the current resume.pdf, and section 7 project mining.
2. **Per job, Claude picks and orders bullets**, keeps the same format:
   - Top line title matched to the job (within truth, e.g. "Senior Frontend Engineer (React, Next.js, AI)").
   - 3-line summary written for that job.
   - Skills row reordered so the job's must-haves come first.
   - Bullets that match the job go to the top of each role.
   - Use the job's own words where they are true ("App Router" vs "Next.js 13+", "LLM" vs "AI").
3. **Rules:**
   - Never add a skill or number Ayush does not have.
   - Aim for roughly 75-80% keyword coverage of the job's must-haves (Jobscan's own advice). Do not stuff keywords or hide white text.
   - ATS safe: one column, normal headings (Experience, Skills, Education), real text in the PDF, no tables for main content, 1-2 pages.
   - Plain English, not AI-sounding.
4. **Output on the job card:** the tailored resume, a short "what changed and why" list, the PDF. File name: `Ayush-Pathak-Resume-<Company>.pdf`.
5. Ayush checks every resume before it goes anywhere.

---

## 7. Finding impact content from local projects

Waiting on: **Ayush to name the project folders on his computer.**

How Claude will do it (read only, no changes to the projects):
1. Read README, package.json, folder structure, config (to know stack and architecture).
2. Read git history: how long Ayush worked on it, his own commits, big features, before/after of big changes.
3. Look for proof of impact: performance work (bundle size, LCP), number of screens/modules, users/clients mentioned in code or docs, tests added, migrations (Pages to App Router), security fixes.
4. Write an **impact bank**: one entry per achievement in STAR form (situation, task, action, result), with "evidence" (file or commit) and "number needed from Ayush" where a number is missing.
5. These feed the master resume, mock interview answers, case studies and blogs.

**Privacy rule:** FITPASS and other company code belongs to those companies. Claude will not copy code or secrets out of it, and the impact bank will only keep high-level descriptions and numbers Ayush approves. It goes in the private dashboard, not in a public repo.

---

## 8. Weekend schedule

Today is Thu 26 Nov.

| Day | Claude | Ayush |
|---|---|---|
| **Thu 26** | This plan. | Answer the open questions below (10 min). Share resume format and project folders if possible. |
| **Fri 27** | Build login + data storage + empty dashboard on a branch of common-portfolio, as a PR (once Ayush says go and adds the repo to this project). Find 15-25 fresh jobs (last 7 days). | Add env variables in Vercel (Claude gives the exact list). Review PR. |
| **Sat 28** | Score all jobs, chance %, import into dashboard. Mine local projects -> impact bank. Master resume. | Confirm numbers in the impact bank (30 min). Pick top 8-10 jobs. |
| **Sun 29** | Mock interviews + tailored resume + cover note for the top 8-10. One live mock session for the #1 job. | Practice 1-2 mocks. Approve each resume and cover note. |
| **Mon 1 Dec** | Ready-to-send list. Nothing sent without Ayush's yes per job. | Send the first 5 approved applications. Ask for referrals at A companies. |

---

## 9. Open questions for Ayush

1. **Minimum salary** (fixed, in LPA) and **notice period**?
2. **Location:** only Delhi NCR + remote, or Bengaluru/hybrid too? Is US night shift ok?
3. **Resume format:** which file/tool?
4. **Local project folders** to mine (paths on your computer).
5. **Build go-ahead:** once research is done, can Claude open a PR on common-portfolio for the dashboard? (The repo needs to be added to this project first.)
6. **Login library:** small custom (`jose`, recommended) or Auth.js v5 like FITPASS?
7. **Storage:** Upstash Redis (fast, recommended for weekend) or Postgres (better for learning)?
8. **Make find-jobs private?** (recommended, since salary and resumes will be discussed)
9. How many applications per day from Monday? (Suggestion: 5 good ones, not 30 random ones.)
