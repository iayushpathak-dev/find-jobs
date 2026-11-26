# Work log

Har step yahan likha jata hai, taaki ye repo memory ki tarah kaam kare. Newest upar.

## 26 Nov 2026 (thread: private job dashboard plan)
- 03:21 UTC: Ayush: by weekend be ready to send applications from Monday. Wants a private jobs dashboard in the portfolio (one fixed user id + password), job priorities, mock interviews per job, chance-of-selection %, resume tailored per job (format coming), impact content from local projects. Research only for now.
- Read existing repo research (shortlist, companies, profile, learning plan, portfolio raw read).
- Web research: Next.js 16 auth (proxy.ts + data access checks), CVE-2025-29927, Upstash Redis free tier, Jobscan/ATS match-rate claims. Raw: research/raw/2026-11-26-dashboard-sources.md.
- Wrote plan/job-dashboard-plan.md: login design (env hash + jose cookie + requireAdmin), storage (Upstash Redis, Zod job schema, import route), scoring 0-100, chance % = shortlist x clear-rounds, mock interview format, resume tailoring rules, project mining method, weekend schedule, 9 open questions.
- 03:23 UTC: Ayush: keep learning my mental model (how I think, work, prompt) for a future product on human psychology. Created ideas/upcoming-product-mental-model.md, seeded from his messages so far. Grows every session.
- 03:31 UTC: Ayush said keep repo private and "ab tu kr jo tuje krna hai". Checked: repo still public at 03:33 (API private=false). Sent him the settings steps again.
- Indeed search (6 searches, 9 JDs read). Scored 7 jobs + skipped list: jobs/scored-2026-11-26.md. Top: Deloitte Senior Consultant React Delhi (79), CONXAI (77, but Indeed date 29 Jun), Mercari (74). Pay and location scores are placeholders until Ayush answers.
- Deloitte interview data (3 pages read, 1 failed). Sample mock: jobs/mocks/deloitte-senior-consultant-react.md (15 questions, 3 rounds). Raw: research/raw/2026-11-26-indeed-search.md.
- Flagged: find-jobs repo is public; suggest making it private before salary/resume data.

## 23 Nov 2026 (thread: 12-day upskill plan)
- 20:46 UTC: Ayush ne poocha: naya title, 12 din ka learning plan, aur mujhe teacher banke padhana.
- Repo padha: market report, profile, shortlist.
- AI SDK latest version check kiya: `ai` v7.0.180. v7 mein system prompt = `instructions`, route `createUIMessageStreamResponse({ stream: toUIMessageStream({ stream: result.stream }) })`.
- Likha: `learning/README.md` (title "Senior Frontend Engineer (React, Next.js, AI)", 12-day plan 24 Nov-5 Dec, project JobMatch AI), `learning/day-01-llm-basics.md`.
- PR #1 khola (branch claude/project-thread-j1la27 -> default branch).
- Ayush: aaj sirf research. Interview rounds company type wise + companies case study/blog mein kya chahti hain.
- Research kiya (web): ~25 pages: interview experiences (ServiceNow, MakeMyTrip, Flipkart, Headout, Walmart GCC, Atlassian, Razorpay, 40-company post), AI interview guides, AI tool policy in interviews, ChatGPT UI design question, case study/blog guides.
- Portfolio poora padha (11 pages). Pata chala: 10+ case studies already hain, blog 0, numbers missing kai jagah, AI assistant already AI SDK v7 + Gemini + Upstash Vector par hai.
- Likha: `research/interview-prep-2026.md`, `research/case-study-and-blog-guide.md`, `learning/day-02-streaming-chat-ui.md`, `TOMORROW.md`, raw notes `research/raw/*`.
- Day 1 lesson mein Gemini key option joda (Ayush ke paas already hai).
- Ayush so gaye; bola sab GitHub par khud save karo. PR #1 merge kiya default branch mein.

- 20:59 UTC: Ayush ne maanga: doosre candidates ka interview data. ~35 public posts padhe (Flipkart, Headout, Jio Hotstar, Freshworks, Delhivery, Netomi, CourseFinder, Kanerika, Fynd, Walmart, Atlassian, Intuit, LinkedIn, Uber, Amazon, OpenAI, xAI, Cursor, Cohere, Perplexity, Distyl, ResortPass, Swiggy/Razorpay/PhonePe/CRED). Raw: research/raw/2026-11-23-candidates-*.md. Summary: research/other-candidates-2026.md. Failed to load: Microsoft, Harness, Uber Glassdoor, Swiggy frontend-junction, Intuit articles.

- 21:06 UTC: Ayush ne maanga: target companies ka candidate interview data. 12 companies search kiye, ~28 pages padhe. Files: jobs/companies/*.md (CONXAI, Mercari India, Mirantis, Hire Hangar, AppsForBharat, VuNet, Ken Research, Avya, no-data-yet for NeoScript/Metadesign/Electrolux/Mavvrik) + jobs/companies/README.md priority table. Findings: CONXAI = CEO + CTO rounds, a senior FE candidate got an offer there; Mercari SDE2 = 2 React problems on HackerRank; Avya low-pay reports; Ken Research is a research firm with old listing.

## Pending / kal
- Ayush ke 9 jawab chahiye (plan/job-dashboard-plan.md section 9). Resume format + local project folders bhi.
- Ayush se case study numbers lene hain (list: research/case-study-and-blog-guide.md section 6).
- Pehla blog saath mein likhna: RAG assistant routing.
- Day 1 lesson karwana. Day 3 lesson banana.
- common-portfolio PR #3 (FITPASS 3+ -> 4+) abhi merge nahi hua.
