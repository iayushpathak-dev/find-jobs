# 12-day plan: Frontend Developer se "Frontend + AI Product Engineer"

Start: Mon 24 Nov 2026. End: Fri 5 Dec 2026.
Time: weekdays 2.5-3 ghante (job ke saath), weekend 5-6 ghante.

## 1. Naya title kya likhna hai

**Resume aur LinkedIn ki top line:**

> Senior Frontend Engineer (React, Next.js, AI)

**LinkedIn headline (plain English, copy-paste ready):**

> Senior Frontend Engineer | React, Next.js, TypeScript | Building AI features with LLMs, RAG and tool calling | 6+ years

Kyun ye, aur "AI Engineer" kyun nahi:
- "AI Engineer" bolne par interviewer ML, Python, model training poochega. Wo tumhara area nahi hai, aur 12 din mein banega bhi nahi.
- "Senior Frontend Engineer" rakhne se tumhare 6+ saal ka experience seedha match hota hai. Bracket mein "AI" daalne se recruiter ki "AI frontend", "LLM", "RAG" waali search mein bhi aa jaoge.
- 12 din baad jab project live ho jayega, tab ye bhi likh sakte ho: **"Senior Frontend / AI Product Engineer"**.

**Jobs search karte waqt ye titles use karo:**
1. Senior Frontend Engineer (AI / LLM)
2. AI Product Engineer
3. Product Engineer (React / Next.js)
4. Senior Full Stack Engineer (Next.js + AI)
5. Frontend Engineer, Generative AI / GenAI UI

## 2. Is role ke liye kya kya aana chahiye

Simple bhasha mein: **"AI Product Engineer" = jo banda AI waala feature shuru se end tak bana ke user tak pahuncha de.** Model banana nahi hai. Model (Claude, GPT, Gemini) ko API se use karke accha product banana hai.

| Skill | Tumhare paas | 12 din mein kya karna hai |
|---|---|---|
| React, Next.js, TypeScript | Strong | Kuch nahi, ye tumhari base hai |
| LLM basics (tokens, prompt, context window) | Thoda | Day 1 |
| Streaming chat UI (AI SDK, useChat) | Nahi | Day 2 |
| Structured output (Zod schema se JSON) | Nahi | Day 3 |
| Tool calling + generative UI | Learning | Day 4 |
| Node + Postgres (DB mein data save) | BFF tak | Day 5 |
| Embeddings + RAG (pgvector) | Kiya hai | Day 6-7, properly aur case study ke saath |
| Agents + MCP basics | Nahi | Day 8 |
| Auth, rate limit, AI security | Auth.js use kiya | Day 9 |
| Playwright testing | Nahi (Jest/RTL hai) | Day 10 |
| Deploy, monitoring, case study | Partly | Day 11 |
| Interview: AI system design | Nahi | Day 12 |

## 3. Ek hi project, 12 din mein

Har din alag chhota demo banane se accha hai ki **ek hi project** roz bada karo. 12 din baad tumhare paas ek live, pinned GitHub project hoga jo interview mein dikha sako.

**Project: JobMatch AI** (apni job search mein bhi kaam aayega)
- Tum job description paste karo, app tumhare resume aur projects se match karke batata hai: kitna fit hai, kya missing hai, kaunse project highlight karne hain.
- Chat UI streaming ke saath, tools (job save karna, match score nikalna), Postgres mein data, RAG tumhare resume/projects par, login, tests, live deploy.

Stack: Next.js (App Router) + TypeScript + Vercel AI SDK v7 + Zod + Postgres (Neon ya Supabase, pgvector ke saath) + Drizzle + Auth.js + Playwright + Vercel.

## 4. Day by day plan

Har din ka format same rahega: **15 min samjho (lesson) -> 2 ghante banao -> 15 min notes/commit.** Har din end mein ek commit GitHub par.

| Day | Date | Topic | Din ke end tak kya ready hoga |
|---|---|---|---|
| 1 | Mon 24 Nov | LLM basics: token, context window, roles, temperature, streaming, cost | Terminal mein chalne waala chatbot (Node + AI SDK) |
| 2 | Tue 25 Nov | Streaming chat UI: `streamText` + `useChat` in Next.js | JobMatch AI ka chat page, text type hota hua dikhe |
| 3 | Wed 26 Nov | Prompting + structured output (Zod) | JD paste karo, JSON milega: skills, years, must-have, nice-to-have |
| 4 | Thu 27 Nov | Tool calling + generative UI | AI "matchScore" tool call kare, UI mein card component dikhe |
| 5 | Fri 28 Nov | Postgres + Drizzle, Route Handlers, chats save karna | Refresh ke baad bhi chat history rahe |
| 6 | Sat 29 Nov | Embeddings + pgvector + chunking (RAG part 1) | Resume aur projects DB mein vectors ke saath |
| 7 | Sun 30 Nov | RAG part 2: retrieval, citations, simple evals | Answer ke saath "ye resume ke kis part se aaya" dikhe + 10 test questions |
| 8 | Mon 1 Dec | Agents (multi-step tools) + MCP basics | Agent jo khud 2-3 tools chain kare; ek chhota MCP server |
| 9 | Tue 2 Dec | Auth.js login, rate limit, prompt injection, API key safety | Login ke baad hi app chale, per-user limit |
| 10 | Wed 3 Dec | Playwright e2e + AI ko mock karke test | 3-4 e2e tests GitHub Actions mein green |
| 11 | Thu 4 Dec | Deploy (Vercel), Sentry/PostHog, README + case study | Live link + case study page portfolio par |
| 12 | Fri 5 Dec | Interview prep: AI system design, common questions, resume/LinkedIn update | Mock interview + updated resume |

Weekend (Day 6-7) ko RAG diya hai kyunki wo sabse bada topic hai aur zyada time maangta hai.

## 5. Kaise padhaunga

- Har din ki lesson file `learning/day-XX-*.md` mein hogi. Pehle simple example (real life waala), phir code, phir "khud karo" task, aur end mein 5 sawal jo interview mein pooche ja sakte hain.
- Tum task karke mujhe bolo "done" ya jo atka wo poocho. Main check karke next day ka lesson khol dunga.
- Agar kisi din time nahi mila, plan ek din aage khisak jayega. Koi problem nahi, bas din skip mat karna, chhota sa hi sahi kuch karna.

## 6. Kya NAHI padhna hai (time bachane ke liye)

- Python, ML math, model training, fine-tuning. Is role ke liye abhi zaroori nahi.
- LangChain jaisa bhaari framework. AI SDK kaafi hai aur Next.js ke saath sabse common hai.
- 5 alag vector DB. Sirf Postgres + pgvector.

## Sources

- AI SDK docs (v7, Next.js App Router quickstart, tools): https://ai-sdk.dev/docs
- Frontend developer to AI engineer: https://www.greatfrontend.com/blog/frontend-developer-to-ai-engineer
- What does an AI product engineer do in 2026: https://zumrywahid.github.io/what-does-ai-product-engineer-do
- Market report in this repo: [../market/market-report-2026-11.md](../market/market-report-2026-11.md)
