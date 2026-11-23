# Interview prep 2026: Senior Frontend / Frontend + AI roles

Research date: 23 Nov 2026. Sources neeche hain. Ye candidates ke apne experience posts hain (LeetCode, Glassdoor, Blind, blogs), to inko "pattern" samjho, guarantee nahi.

## Short answer: pattern same hai kya?

**Haan, 70% same hai.** Lagbhag har company mein ye 5 cheezein aati hain:

1. **Machine coding** (sabse important, har jagah). 60-90 min mein React ya vanilla JS mein ek chhota feature banana.
2. **JavaScript deep** (Promise, event loop, closures, polyfills).
3. **Frontend system design** (HLD + kabhi LLD).
4. **Project deep dive** (tumhare resume ke project ka architecture, decisions, trade-offs). MakeMyTrip mein 2 rounds isi par the.
5. **Hiring manager / behavioral** (ownership, mentoring, conflict, trade-offs).

**Jo badalta hai:** DSA kitna, AI ke sawal kitne, aur AI tools allowed hain ya nahi. Ye company type par depend karta hai (neeche table).

## Company type ke hisaab se rounds

| Company type | Examples | Rounds (typical) | DSA | Khaas baat |
|---|---|---|---|---|
| Indian product / unicorn | Flipkart, MakeMyTrip, Razorpay, Headout, Swiggy | 3-5: machine coding, JS, system design/product design, HM | Light to medium (LeetCode medium) | Machine coding + resume project ka HLD sabse heavy |
| GCC (global capability center) | Walmart Global Tech, Atlassian, ServiceNow, JPMC | 3-6: DSA, JS + polyfills, system design, HM | Medium, kabhi 1 hard | Zyada structured. Walmart SDE-3 frontend: 2 medium + 1 hard DSA |
| Atlassian (special) | Atlassian India | Karat screen (JS + CSS output questions), React machine coding, JS (Promises, async, localStorage), HLD, 2 managerial | Frontend mein almost nahi | "Sirf output aana kaafi nahi", code optimized aur clean chahiye |
| Global remote / US startups | Apollo.io, Levels.fyi, Hinge Health | OA/take-home, debugging round, system design, culture | Low | Debugging round (12 bugs, time limit), 1-2 din ka assignment |
| AI startups / AI-first product | Mavvrik, Conxai, Ramp, Granola, LangChain | Screen (RAG/prompting basics), take-home (LLM feature + eval), live coding/debug, system design, product sense | Low | "Build karo aur measure karo". Evals, RAG, agents, streaming UI |
| Service companies | TCS, Infosys type | Ye research mein data nahi mila. Tum product/GCC target kar rahe ho, to skip. | | |

## Har round mein kya aata hai (real examples)

### 1. Machine coding (sabse zyada practice yahin)
Real sawal jo pooche gaye:
- Autocomplete / search with **debounce + AbortController** (purani request cancel), loading/empty/error states. (MakeMyTrip, ServiceNow)
- Stopwatch: start, pause, reset. (MakeMyTrip)
- Kanban board **vanilla JS + CSS** mein, 90 min. (Headout)
- JSON se **dynamic form** banana. (Razorpay 2025)
- **Tabs component** jaise Material UI. (Razorpay 2024)
- Nested comments (recursion, deep threads). (ServiceNow, Atlassian)
- Infinite scroll / 100k items virtualization, carousel, modal manager, chat UI with message status. (general guides)
- **Naya AI waala:** streaming function diya hai, uske around ChatGPT jaisa UI banao, aur beech mein naya message aaye to purana stream cancel karo. (OpenAI, Feb 2026)

Kya check karte hain: edge cases, clean component split, a11y (keyboard), race conditions, code readable hai ya nahi.

### 2. JavaScript
- Custom **Promise** likho (Flipkart). Promise-based **retry** polyfill (Walmart).
- Polyfills: `debounce`, `throttle`, `Promise.all`, `bind`, `map/reduce`.
- Event loop output questions, closures, `this`, async/await.
- Browser history with back/forward N steps design karo (Walmart).
- "Bundler kya hai? Webpack mein dependency injection kaise?" (MakeMyTrip)
- React: reconciliation, `useMemo` kab, unnecessary re-render kaise roko, memory leak debug, stale closure.
- Sawal: "Search effect mein `ignore` flag kyun hota hai?" Jawab: purani query ka late response naye result ko overwrite na kare.

### 3. Frontend system design
Real prompts:
- Nested comments system, notification panel (real-time, consistency). (ServiceNow)
- Google Sheets (formulas, collaboration, offline). (Headout)
- Figma / Notion block editor, real-time chat with optimistic updates, photo gallery, design system. (guides)
- **Design ChatGPT jaisa chat frontend with streaming.** (OpenAI, Waymo, bahut common ho raha hai) -> neeche poora answer outline.
- Internal "ChatGPT Playground": model select, parameters edit, shareable presets. (OpenAI)

Framework jo har design mein use karo (RADIO): **R**equirements -> **A**rchitecture (components) -> **D**ata model (state) -> **I**nterface (API contract) -> **O**ptimizations (perf, a11y, security).

### 4. Project deep dive (tumhara sabse strong round ho sakta hai)
MakeMyTrip ne 30-40 min sirf current project ka HLD Excalidraw par banwaya. Headout HM round: tech debt, ownership, user impact, trade-offs.
Tumhare paas already strong material hai (portfolio case studies). Bas ye 4 projects ke diagram ready rakho:
1. FITPASS BFF (200+ service map, gRPC events)
2. Partner Studio (20+ partners, Auth.js, 3 data paths, WebView)
3. Liveness check (TF.js + MediaPipe, GPU fallback, 5 flows)
4. AI assistant (RAG, routing before the model, Upstash Vector)

### 5. HM / behavioral
- Mentoring 2 juniors ki story
- Backend/design ke saath disagreement ki story
- Deadline tight thi, kya cut kiya
- Production bug jo tumne pakda/fix kiya
- "Job kyun badal rahe ho?"

STAR format: Situation, Task, Action, Result (number ke saath).

### 6. AI ke sawal (ab normal frontend interviews mein bhi aa rahe hain)
- "AI tools use karte waqt token usage kaise optimize karte ho?" (MakeMyTrip 2026, frontend role!)
- "200 page PDF aur ek sawal. Enter dabane se answer tak kya kya hota hai?"
- "RAG system design karo. Kaise pata chalega ki accha kaam kar raha hai?" (evals, recall@k, faithfulness)
- "Agent kuch inputs par infinite loop mein chala jaata hai, debug karo."
- "Customer bolta hai bot dumb lagta hai. Kya karoge?" (product sense)
- "Model ka output render karte waqt XSS risk?" (OWASP LLM05), "Prompt injection kaise rokoge?" (OWASP LLM01)
- Take-home example: 50 markdown docs, Q&A system banao, 20 sawal ka eval set, recall@5 aur faithfulness report karo.

## AI tools interview mein allowed hain?

Company to company alag hai, aur sources aapas mein bhi match nahi karte. **Har round se pehle recruiter se likhit mein poochho.**
- Allowed / encouraged (reports ke hisaab se): Canva (AI-assisted coding round), Shopify, kuch AI startups, Google ka pilot round (Gemini ke saath).
- Mostly band: Amazon, Meta (official guide), Apple, banks, quant firms. Live rounds aam taur par AI-off, take-home mein zyada allowed.
- Jab allowed ho, to judge karte hain: problem ko todna, AI ko chhota bounded kaam dena ("sirf hook likho"), output ko PR ki tarah review karna, test likhna. AI ka code bina padhe paste karna = reject.
- Hidden AI use (tab switch, paste) proctoring pakad leta hai.
- Sawal tayyar rakho: "Tum AI tools kaise use karte ho?" Tumhara Claude Code workflow page (portfolio par hai) yahan kaam aayega.

## Design answer: "ChatGPT jaisa chat frontend with streaming"

Ye sawal tumhare target roles mein sabse likely hai. Isko yaad nahi, samajh ke rakho.

1. **Requirements poochho:** refresh ke baad chat rehni chahiye? Stop/regenerate/edit chahiye? Markdown + code blocks? Context window bhar jaaye to? Mobile? File upload?
2. **Components:** stable page shell (sidebar, header) alag, streaming answer panel alag, taaki har token par poora page re-render na ho. MessageList, Message (parts render), Composer, StopButton.
3. **State:** messages array (id, role, parts), ek `status` (submitted/streaming/ready/error), booleans ka jungle nahi.
4. **Transport: SSE vs WebSocket.** Chat mein data mostly server -> client aata hai, aur har message ek naya HTTP request hai. Isliye HTTP streaming / SSE simple hai: normal auth cookies, proxies/CDN ke saath chalta hai, reconnect easy. WebSocket tab jab dono taraf continuous real-time chahiye (multi-user collaboration, live presence).
5. **Cancel:** AbortController se stream band karo. Naya message beech mein bheja to purana stream cancel. (Interviewers specially dekhte hain.)
6. **Rendering perf:** tokens ko buffer karke `requestAnimationFrame` mein ek baar render; sirf last message re-render ho (memo); lambi chat mein virtualization; half-open code fence ko special handle karo.
7. **Scroll:** auto-scroll sirf tab jab user bottom par hai.
8. **Errors:** stream shuru hone se pehle fail vs beech mein fail; partial text rakho + Retry; user ko generic message, server ka error nahi.
9. **Security:** model ka HTML kabhi seedha render nahi (`dangerouslySetInnerHTML` nahi), markdown sanitize; tool/structured output ko schema se validate karo, fail ho to plain text. Auth, billing, irreversible actions model ke haath mein nahi.
10. **A11y:** `aria-live="polite"`, par har token announce nahi, poora message hone par.
11. **Metrics:** time to first token (TTFT) sabse important, phir total time, error rate, stop rate.
12. **Follow ups:** persistence (DB), network drop par resume, context window bhar gaya to purane messages summarize.

## Prep checklist (12-day plan ke saath)

Roz plan waale kaam ke baad **30-45 min interview practice**:

| Day | Extra practice |
|---|---|
| 1 | 2 polyfills: debounce, throttle |
| 2 | Machine coding: autocomplete with debounce + AbortController (45 min timer) |
| 3 | Promise.all + Promise retry polyfill |
| 4 | Machine coding: nested comments |
| 5 | Event loop output questions (10) |
| 6 | DSA: sliding window (2 medium) |
| 7 | Design: ChatGPT chat frontend (upar waala outline, khud bolke practice) |
| 8 | Machine coding: Tabs + dynamic form from JSON |
| 9 | Design: notification panel |
| 10 | DSA: linked list + intervals (2 medium) |
| 11 | Project deep dive: 4 diagrams Excalidraw mein |
| 12 | Mock interview (main loonga): 1 machine coding + 1 design + HM sawal |

## Sources
- 40 companies senior frontend experience: https://leetcode.com/discuss/post/7580886
- Frontend interview guide 2026: https://www.techinterview.org/post/3233474937/frontend-engineering-interview-guide-2026/
- Applied AI engineer interviews 2026: https://www.techinterview.org/post/3233476824/ai-engineer-interview-rag-agents-evals/
- ServiceNow senior frontend (Feb 2026): https://leetcode.com/discuss/post/7711064/servicenow-senior-software-engineer-fron-6gsw/
- MakeMyTrip SSE frontend (Oct 2026): https://leetcode.com/discuss/post/8565477/make-my-trip-interview-experience-for-ss-qp5f/
- Flipkart senior frontend: https://www.jointaro.com/interviews/companies/flipkart/experiences/senior-frontend-engineer-india-september-16-2025-declined-offer-positive-f89c4ee4
- Headout lead frontend (Apr 2026): https://leetcode.com/discuss/post/7792155/headout-frontend-interview-experience-by-d9b3/
- Walmart Global Tech SDE-3 frontend (Jan 2026): https://devtools.tech/blog/walmart-global-tech-frontend-interview-experience-sde-3---rid---p7M1epgvyBQeNoz32zr9
- Atlassian senior frontend (Mar 2025): https://www.jointaro.com/interviews/companies/atlassian/experiences/senior-frontend-developer-bengaluru-march-1-2025-no-offer-positive-7190963f/
- Razorpay (Glassdoor): https://www.glassdoor.co.in/Interview/Razorpay-Interview-E1146550-RVW98995431.htm
- AI tools in interviews: https://www.greatfrontend.com/blog/ai-assisted-coding-interviews-for-frontend-developers , https://www.techinterview.org/post/3233474911/ai-tool-policy-tracker-tech-companies-2026/
- ChatGPT UI design prompts: https://prachub.com/interview-questions/design-the-frontend-of-an-ai-chat-application-with-streaming-replies , https://prachub.com/interview-questions/design-chatgpt-streaming-replies-over-sse-and-rendering-long-conversations
- AI in frontend system design: https://www.educative.io/courses/grokking-frontend-system-design-interview/how-ai-has-reshaped-frontend-system-design-and-interviews , https://www.educative.io/blog/openai-frontend-engineer-interview
- Frontend to AI engineer (job posts, OWASP LLM): https://www.greatfrontend.com/blog/frontend-developer-to-ai-engineer
