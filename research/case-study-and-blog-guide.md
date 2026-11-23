# Case studies aur blogs: companies kya dekhna chahti hain (2026)

Research date: 23 Nov 2026. Kal ki writing session isi file se shuru hogi.

## 1. Hiring manager case study mein kya dhoondhta hai

Ek line mein: **"Is bande ne soch ke decision liya, ya bas stack ka naam likh diya?"**

Unko chahiye:
1. **Specific problem.** "Company ko naya dashboard chahiye tha" nahi. "20+ partners ke liye ek hi codebase, purane Android WebViews par" haan.
2. **Constraints.** Purana backend jo badal nahi sakte, deadline, team size, purane phones.
3. **Decisions with "why this, not that".** Jo choose kiya AUR jo reject kiya, dono, 2-4 lines mein. 3-5 bade decisions kaafi hain. Linter jaisi chhoti cheez skip.
4. **Trade-offs.** Is decision se kya nuksaan hua, aur kab ye decision galat ho jayega.
5. **Result with numbers.** Ek headline number + 2 supporting numbers + 1 line ka qualitative result. Number nahi hai to jhooth mat likho, likho kaunsi problem khatam hui.
6. **"What I'd do differently."** Apne kaam ki asli critique. Ye seniority ka sabse bada signal hai.
7. **Diagram.** Ek simple Excalidraw architecture diagram, ya product ka real screenshot.

**Mistakes jo reject karwaati hain:**
- Sirf stack badges (Next.js, Tailwind, ...) bina "kyun" ke
- Fake ya badha-chadha ke metric, team ka kaam "maine kiya" bolke
- Docs ko copy karke tutorial likhna
- Ek blog likh ke chhod dena
- Shuru mein lambi background story, asli point neeche dabba hua
- Sab kuch perfect dikhana. Bugs, dead ends aur follow-up work dikhane se trust badhta hai.

## 2. Case study template (har project ke liye)

Length: **800-1,500 words** (~1,200 best). 2,000 se upar ho to 2 post bana do.

```
# <Project name>: <one line jo problem + result bataye>

**Summary (3 lines):** kya banaya, kiske liye, kya result aaya.
**My role:** maine kya kiya (team ka nahi).

## The problem
Ek specific paragraph.

## Constraints
- 3-4 real constraints

## Architecture
Diagram + 1 paragraph: data kaise flow hota hai.

## Key decisions
| Picked | Rejected | Why |
|---|---|---|
| ... | ... | ... |

## Trade-offs
Kya chhoda, kab ye galat ho jayega.

## How I checked it works
Tests, monitoring, metrics, manual QA.

## Result
Headline number + 2 supporting numbers + 1 line.

## What I'd do differently
Honest 2-3 points.
```

Tip: abhi se har project repo mein `decisions.md` rakho. Jab bhi koi bada choice karo, 3 line likh do: options, constraint, kyun. Baad mein case study 10 min mein ban jaati hai.

## 3. Blog kahan publish karein

- **Main jagah: apni site** (ayushpathak.co.in/blog). Wahan `/blog` page already hai, bas posts nahi hain.
- Cross-post: dev.to ya Hashnode, **canonical link** apni site ka rakh ke.
- Har post ke end mein GitHub aur LinkedIn link. LinkedIn par har post ka 5-line summary daalo.
- Achhe titles specific hote hain: "How I cut our API p99 from 800ms to 120ms" > "Introduction to caching".

## 4. Tumhare portfolio ki abhi ki position (23 Nov 2026 ko padha)

**Accha:** 10+ case study pages already hain aur detail bahut achhi hai (architecture, trade-offs, limitations). Ye bahut logon se aage hai.

**Gaps (kal fix karne hain):**

| Case study | Kya missing hai |
|---|---|
| Partner Studio | Koi performance number nahi (load time, Lighthouse partner app ka). "What I'd do differently" nahi. Diagram? |
| BFF (200+ services) | Latency, cache, kitne API calls bache, payload kitna chhota hua: koi number nahi |
| FITPASS website | Sabse strong. LCP 1.6s mobile, INP 110ms, CLS 0, SEO 100 (23 Nov 2026 PSI). Bas "before" number mil jaye to killer ban jayega |
| Nutrition Dashboard | ~50 routes, 60,000+ users. Missing: config-driven se kitna time bacha (naya screen pehle kitne din, ab kitne) |
| Liveness check | Engineering detail best hai. Missing: pass rate, kitne check-ins, GPU fallback kitne devices par laga, Luxand ke paise kitne bache |
| AI assistant (RAG) | Missing: model naam, embedding model, chunk size, top-K, threshold, **eval set ke results**. AI roles ke liye ye sabse important page hai |
| QTickets, LOGITRACK | Sirf 1 line. Chhota case study ya chhod do |
| Blog | 0 posts. Sirf "planned topics" |

Inconsistency jo fix karni hai: homepage "3+ years at FITPASS" vs baaki jagah "4+" (PR #3 common-portfolio mein already fix bheja hai, merge baaki). Fitshop: resume mein "membership platform rebuilt" vs page par "e-commerce store".

## 5. Kal ke liye blog list (priority order)

Rule: wahi likho jo tumne khud production mein kiya. Ye sab tumhare real kaam se hain, aur AI/frontend dono roles mein recruiters inhe search karte hain.

1. **"Face liveness in the browser on low-end Android WebViews"** (TF.js + MediaPipe, GPU blocklist + CPU fallback, Laplacian sharpness, paid API se pehle local gate). Bahut unique hai, kam log ye likhte hain.
2. **"Routing before the model: how my RAG assistant avoids bad answers"** (keyword router, injection ko bina model call ke rokna, "I don't have that information", content-hash re-index). AI roles ke liye #1 post.
3. **"One BFF for 200+ legacy services in Next.js Route Handlers"** (service map, response filtering, gRPC events with protobuf Any).
4. **"Core Web Vitals on a 200+ route Next.js site"** (LCP preload per device, reserved aspect ratio, lab vs field data ka farak).
5. **"One Next.js codebase for 20+ partner apps inside WebViews"** (Auth.js signed links, 3 data paths, iOS keyboard + safe area).
6. Day 11 ke baad: **"JobMatch AI: what I learned building an AI SDK app with tools, RAG and evals"**.

## 6. Kal tumse ye numbers chahiye (inke bina case study kamzor rahegi)

Jitne yaad hain utne. Approx bhi chalega, bas honest ho:
- RAG assistant: kaunsa Gemini model, embedding model, chunk size, top-K, threshold, eval set mein kitne sawal aur kitne sahi
- Liveness: roz/mahine kitne face checks, pass rate, kitne devices CPU fallback par gaye
- BFF: ek page par pehle kitni API calls / payload size, ab kitni
- Nutrition dashboard: naya screen banane mein pehle vs ab kitna time
- Website: migration se pehle koi Lighthouse/LCP number yaad hai?
- Partner Studio: sabse bada partner kaun sa (naam nahi chahiye, size chahiye: kitne users)

## Sources
- https://slategit.com/blog/documenting-technical-tradeoffs-in-a-portfolio-case-study
- https://saranzafar.vercel.app/blog/technical-case-studies-recruiters-actually-read
- https://www.greatfrontend.com/blog/frontend-developer-portfolio
- https://slategit.com/blog/developer-technical-blog-as-hiring-signal
- https://algomaster.io/learn/job-search/technical-blogging
- https://dev.to/therizwansaleem/designing-a-career-portfolio-that-signals-real-seniority-beyond-generic-tech-skills-2m04
- Portfolio: https://www.ayushpathak.co.in (projects, resume, blog pages read on 23 Nov 2026)
