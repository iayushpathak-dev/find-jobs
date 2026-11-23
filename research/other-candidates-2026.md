# Doosre candidates ke interview: kya poocha, kya galat hua, kitna mila

Research date: 23 Nov 2026. ~35 public posts padhe (LeetCode Discuss, Glassdoor, Blind, Medium, Substack, prep sites). Raw notes: [raw/](raw/) folder ki `2026-11-23-candidates-*.md` files.
Dhyan rakho: ye log apna experience khud likhte hain, aur kuch sites prep tools bechti hain. Pattern samjho, har line guarantee nahi.

## 1. Company wise: kaunse rounds, kya poocha

| Company | Role, saal | Rounds | Asli sawal | Result |
|---|---|---|---|---|
| Flipkart | Frontend SDE-2, 2025 | 5: machine coding, PS-DS, UI tech, product sense, HM | Plain JS app + code review; promises parallel aur sequential bina async/await; curried sum(2)(3)(4)(); Promise.all from scratch; 2-player game features P0/P1/P2; Stripe jaisa payment gateway kaise jodoge | Reject (product sense round mushkil laga) |
| Headout | SDE3/Lead, 2026 | 4: 3 machine coding + design | List virtualization + sort/filter; stacked toast; drag se reorder TODO; Google Sheets design | - |
| Jio Hotstar | SDE-2 Frontend, 2025-26 | Tech, machine coding, HM | Event loop / execution order; **Dropdown component** (a11y, edge cases) | Reject: Noida se Bangalore relocation ka doubt, tech nahi |
| Freshworks | Senior Full stack, 2026 | DSA + resume, frontend | Stock Span I/II/III; `left` vs `transform` kaunsa fast aur kyun; async vs defer; Shadow DOM vs Virtual DOM; tooltip sirf CSS; Array prototype par flatten; React Fiber | Reject R2 ke baad ("why" nahi bata paaye) |
| Delhivery (Gurgaon) | Frontend, Apr 2026 | 3 | setTimeout+Promise+async output; Fiber; CORS; **draggable div**; "AI se tumhara purana kaam kaise fast hota?"; puzzles | - |
| Netomi (Gurgaon) | Frontend 2, Apr 2026 | 7-8 rounds | Memory game; e-commerce cart design; traffic light; WhatsApp encryption design (VP) | Reject: VP ne jawab "generic, AI generated" bole |
| CourseFinder AI | Senior React, May 2026 | 5 | Longest substring K distinct; CRUD todo; Redux vs Context; CSS 2-column fixed + scroll; cart+inventory LLD; **buggy code review** | Comp fix hone ke baad reject |
| Kanerika | Frontend, 3.5 yrs, 2025 | 4 + surprise client round | 30+ JS trivia: NaN===NaN, typeof null, IIFE, currying, Web Workers, Promise.allSettled, micro-frontends | Reject |
| Fynd | Senior Frontend | 2-4 | useMemo vs useCallback, debounce, Promise.all | Ghosting, kharab experience reports |
| Walmart GCC | SDE-3 Frontend, Jan 2026 | 3 | 2 medium + 1 hard DSA (sliding window max); Promise retry polyfill; browser history back/forward N | - |
| Atlassian | Senior/Staff | Karat + 4-5 | JS/CSS output; UI from picture; tic-tac-toe; folder tree; "large React app optimize karo"; sprint board design | Mostly no offer, process acha |
| Intuit | Staff -> Senior downlevel | 1 round | Zyada **GenAI kaam** ke sawal; React virtual DOM in-memory banao; project architecture | Downlevel |
| LinkedIn | Senior IC3, 7 yrs | 7 | Widget from image (a11y); autocomplete design + code; calculator; iframe widget pros/cons; DOM node child check; Kadane; clearAllTimeout; infinite scroll; A/B test design | Reject: DSA mein hint liya, design mein senior signal kam |
| Uber | Senior Frontend screen | - | **React mein Chat UI, async API khud mock karo** | - |
| Amazon | Frontend Eng I | OA + 2 | BST triplet sum 0; matrix most 1s; UI recreate HTML/CSS | Reject (DSA zaroori hai) |
| OpenAI | Frontend | 4-6 | **Streaming function par ChatGPT UI**, beech mein naya request, ek-ek char display; toast; Playground design with presets | - |
| xAI | Frontend | - | React typeahead: async, keyboard, stale result/race, no libraries | - |
| Cursor | Eng | phone + onsite | Streaming LLM edits as tokens aaye; diff tracking; context retrieval | AI ka unchecked code = reject |
| ResortPass | Senior FE, 10+ yrs | 3 | Decode String; React code critique; Next.js filters synced with query params | - |

## 2. Log reject kyun hue (sabse kaam ki cheez)

1. **"Kya" bataya, "kyun" nahi.** Freshworks: concepts pata the, reason nahi. Fix: har answer mein "kyunki..." bolo.
2. **Generic / AI jaisa jawab.** Netomi VP ne seedha bola. Fix: har jawab apne project ke real example se (FITPASS BFF, liveness, Partner Studio).
3. **Senior signal kam.** LinkedIn: design mein trade-offs aur scale nahi bole. Fix: RADIO framework + har decision ka trade-off.
4. **DSA mein hint lena.** LinkedIn, Amazon. Fix: roz 1-2 medium (sliding window, stack, tree, intervals).
5. **Relocation / notice period.** Jio Hotstar (Noida -> Bangalore), Rippling (lambi notice). Fix: recruiter call mein hi clear karo: notice period kitna, relocate karoge ya nahi.
6. **Product sense round ko halka lena.** Flipkart. Fix: "P0/P1/P2 features" aur MVP soch practice karo.
7. **AI tool par zyada bharosa.** Amazon (Copilot), Cohere, Cursor. Fix: AI allowed ho tab bhi code khud padho aur samjhao.
8. **Bahut saare interviews ek saath, thak gaye.** Uber L5 reject after burnout. Fix: hafte mein 3-4 se zyada interviews mat rakho.
9. **Process lamba, ghosting.** Fynd, Hotstar, CourseFinder. Fix: ek saath 4-5 companies chalao, ek par depend mat raho.

## 3. Sabse zyada repeat hone waale sawal (inko pakka karo)

**Machine coding (top 10):**
1. Autocomplete / typeahead (debounce, AbortController, keyboard, race) — 6+ companies
2. Chat UI with streaming + cancel + naya request mid-stream — Uber, OpenAI, AI cos
3. Dropdown / Tabs / Toast / Modal component with a11y
4. Draggable div / drag to reorder list
5. Virtualized list with sort + filter / infinite scroll
6. Nested comments / folder tree
7. Todo CRUD, stopwatch, memory game, tic-tac-toe
8. Dynamic form from JSON
9. UI from image (plain HTML/CSS)
10. Filters synced with URL query params (Next.js)

**JS (top):** Promise.all / allSettled / retry polyfill, promises sequential without async/await, debounce/throttle, curry, flatten, event loop output, this / closures / prototypes, clearAllTimeout.

**React:** reconciliation + Fiber, useMemo vs useCallback, why renders twice, Redux vs Context vs Zustand, large app optimize, RSC vs client, hydration mismatch.

**Browser/CSS:** transform vs left perf, async vs defer, critical rendering path, CWV (LCP, INP, CLS), CORS, flex centering, CSS-only tooltip.

**Design:** Google Sheets, ChatGPT UI / Playground, notification panel, autocomplete, e-commerce cart, sprint board, news feed.

**AI (naye):** "AI se kaam fast kaise kiya?", token cost kaise kam, RAG with citations, eval kaise, streaming UI INP kharab na kare, LLM key client par kyun nahi.

## 4. Salary data jo mila

| Company | Level | Range | Source |
|---|---|---|---|
| Swiggy | Senior (5-8 yrs) | Rs 40-55 L base | OnlyFrontendJobs (LeetCode/Levels.fyi se) |
| Swiggy | Staff (8+) | Rs 55-90 L base | same |
| Razorpay | Senior | Rs 27-45 L base | same |
| Razorpay | Staff | Rs 45-65 L base | same |
| Gojek | Lead Frontend, 9 yrs (~2021) | ~65 L | Blind |
| Compass | SSE IC3, 9 yrs (~2021) | ~80 L | Blind |
| Uber | - | Competing offer dikhane par joining bonus badha | Intervue |

Market report wala range bhi yaad rakho: product/GCC 5-8 yrs Rs 18-40 LPA. Upar wale top companies ke numbers hain.

## 5. Ayush ke liye seedhe lessons

- Tumhara **sabse bada hathiyaar project deep dive** hai. Har jagah 15-40 min isi par jaata hai. Portfolio ke case studies se 4 diagram ready karo (TOMORROW.md mein hai).
- **Chat UI with streaming** ab "frontend + AI" roles ka standard machine coding sawal hai. Day 2 lesson exactly yahi sikhata hai, isko 45 min mein bina dekhe banane ki practice karo.
- **Delhi NCR (Delhivery, Netomi)** mein AI usage ke sawal aur puzzles aa rahe hain, aur VP/CTO tak rounds jaate hain.
- Recruiter se pehli call mein poochho: kitne rounds, DSA hai ya nahi, AI tool allowed hai ya nahi, location/hybrid.
- Notice period aur relocation ka jawab pehle se tay rakho.

## Sources (sab raw notes mein bhi hain)
- https://roundz.substack.com/p/flipkart-interview-experience-frontend-engineer-sde2
- https://learnersbucket.com/interview/headout-sde3-lead-frontend-interview-questions-2026/
- https://medium.com/frontend-army/hyperface-frontend-interview-experience-sde-3-bengaluru-b6e29ba3be91
- https://leetcode.com/discuss/post/7598082/ (Jio Hotstar)
- https://leetcode.com/discuss/post/8139568/senior-software-engineer-reactjs-coursef-24nn/
- https://leetcode.com/discuss/post/8434484/freshworks-senior-software-engineer-full-u7dt/
- https://www.glassdoor.sg/Interview/Delhivery-Interview-E513409-RVW104020062.htm
- https://www.glassdoor.sg/Interview/Netomi-Interview-E2854590-RVW103763669.htm
- https://www.glassdoor.co.in/Interview/Fynd-Interview-E871023-RVW95256152.htm
- https://leetcode.com/discuss/interview-experience/7174297 (Kanerika)
- https://www.teamblind.com/post/seeking-pointers-for-intuit-and-atlassian-senior-frontend-engineering-interview-x5rf3u0v
- https://www.glassdoor.ca/Interview/Atlassian-Interview-E115699-RVW98002824.htm
- https://www.teamblind.com/post/india-frontend-interviews-and-offer-journey-hjdqt5v4
- https://leetcode.com/discuss/post/7157626/ (Fanatics)
- https://roundz.substack.com/p/interview-experience-152-linkedin-sde3-ic3-frontend-engineer
- https://www.intervue.io/blog/uber-interview-experience
- https://frontendlead.com/discuss/t/uber-senior-frontend-engineer-phone-screen/3429
- https://leetcode.com/discuss/interview-question/6329840/ (Amazon)
- https://www.aceround.app/blog/razorpay-phonepe-swiggy-cred-interview-india/
- https://www.finalroundai.com/blog/swiggy-interview-process
- https://github.com/ombharatiya/FAANG-Coding-Interview-Questions/blob/main/AI-Companies-Interview-Questions.md
- https://www.designgurus.io/blog/openai-frontend-engineer-interview
- https://www.greatfrontend.com/interviews/company/openai/questions-guides
- https://prachub.com/interview-experiences/distyl-seniorplus-ai-engineer-interview-experience-a-whisper-streaming-take-home-then-system-design-and-a-deploy-deep-dive
- https://gitgood.dev/blog/cracking-the-ai-startup-interview-2026
- https://frontendlead.com/discuss/t/resortpass-senior-frontend-engineer/3234
- https://www.onlyfrontendjobs.com/blog/frontend-developer-interview-questions-2026
- https://guibai.dev/a/7675480888482594850/
- Not loaded: Microsoft 2026 (Medium), Harness 8 rounds (Medium), Uber Glassdoor, Swiggy frontend-junction, Intuit articles (off-site).
