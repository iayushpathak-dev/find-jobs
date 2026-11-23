# Raw notes: interview experience sources (read 23 Nov 2026)

Candidate anecdotes, not surveys. Summary lives in ../interview-prep-2026.md.

## leetcode.com/discuss/post/7580886 (~40 companies, 6.5+ yrs, offers: MakeMyTrip, Agoda Bangkok, Conxai)
- Apollo.io 5 rounds; R3 debugging with 12 bugs (fixed 10, rejected). Sumo Logic 4 rounds, out after system design. Twilio out after R2 system design. Levels.fyi 3 rounds + ~1.5 day assignment + culture. Hinge Health out after OA (simple frontend task). Avoma: very specific JS/library questions. HighLevel: build Next.js app in R1. Amazon: frontend OA 2 questions, then ghosted. D.E. Shaw India: OA 1 DSA full + 1 partial.
- India loops "focused on identifying gaps"; overseas loops on knowledge, approach, communication. Rakuten: reconnect after 6 months due to 6+ month gap.

## techinterview.org frontend guide 2026 (May/Jul 2026)
- Rounds: machine coding 45-60 min, JS/TS, React, CSS architecture, a11y, browser internals, performance, frontend system design.
- Machine coding: autocomplete with debounce + keyboard nav; infinite scroll with virtualization; drag and drop; carousel; modal manager; chat UI with message status.
- JS/TS: closures, prototypes, this, promises, event loop, TS conditional/mapped types, generics. React: hook pitfalls (stale closures, infinite loops), state mgmt, RSC vs client, Suspense, concurrent, memoization. Perf: LCP, INP, CLS, TTFB, bundle analysis, SSR/SSG/CSR.
- System design: Figma-like editor, Notion block editor, real-time chat with optimistic updates, photo gallery, design system.
- AI tools increasingly allowed in machine coding; confirm with recruiter.

## techinterview.org applied-AI engineer (Jul 2026)
- Loop: phone screen (retrieval + prompting), take-home (build + measure LLM system), live coding/debug, system design (eval + serving), customer/product sense.
- Qs: 200-page PDF, enter to answer walk-through; take-home 50 markdown docs + 20-question eval, report recall@5 and faithfulness; agent loops forever, debug; design support assistant, how do you know it helps; customer says bot feels dumb.
- RAG: structure-aware vs fixed 512-token chunks; k trade-off; when retrieval is wrong tool; recall@k, precision@k, MRR/NDCG. Evals: faithfulness, relevance, deterministic + LLM-judge, judge biases (length, position, self-preference), calibrate with human labels. Agents: tracing, cap tool calls + spend, replay failed runs; latency: small router model, semantic cache, parallel tools; 800ms target example.

## ServiceNow Senior SWE Frontend (Feb 2026)
- R1: Merge Intervals, Copy List with Random Pointer, then nested comments design. R2: autocomplete (debounce, API, loading/empty). R3 (2 interviewers): notification panel design (real-time, consistency), project deep dive, rendering 100k messages (virtualization, dynamic heights, scroll). Hiring paused after.

## MakeMyTrip SSE-1 Frontend (~3 yrs, selected, Oct 2026)
- R1: Minimum Platforms DSA; React stopwatch; resume. R2: HLD of current project in Excalidraw (15-20 min); search with debounce + AbortController. R3: detailed project HLD (30-40 min); "What is a bundler?", DI in Webpack; "How do you optimize token usage when working with AI tools?"; Git conflicts, technical disagreements.

## Flipkart Senior Frontend (Sep 2025, declined offer)
- 5 rounds: machine coding; DSA (LC medium, lenient); JS: implement custom Promise; product design; HM. Asked: website performance trade-offs and accessibility.

## Headout Lead Frontend (10 yrs, Apr 2026, no offer)
- 3 x 90 min: kanban board in vanilla JS + CSS; HLD + LLD Google Sheets (formulas, collaboration, offline); HM: code review (perf, security, maintainability), project deep dive (tech debt, ownership, impact, trade-offs), culture (mentoring, cross-functional conflict). Product engineering mindset.

## Walmart Global Tech SDE-3 Frontend (devtools.tech, Jan 2026)
- R1 DSA: 2 medium + 1 hard: compare two linked lists; longest substring without repeating chars; sliding window maximum (deque).
- R2 JS + web + design: closures, event loop, promises, polyfills from scratch; Promise retry method; browser history with back/forward N steps; SSR, LCP, perf trade-offs.
- R3 HM: leading frontend projects, React/state/build tool decisions, working with design/backend/QA, design systems at scale, data-heavy e-commerce UI.
- (Walmart SSE backend Oct 2025: DSA, LLD restaurant reservation, HLD Netflix, HM. Not frontend.)

## Atlassian India Senior Frontend
- Mar 2025 (jointaro): Karat screen (JS + CSS output questions, 1 CSS impl, 1 JS coding); React machine coding (edge cases); JS (Promises, async, localStorage, optimization); HLD; 2 managerial. "Output alone does not guarantee selection."
- Blind 2022: no DSA; 3 rounds JS, system design, React; JS mostly promises/async; API calls + caching. Unverified: nested comments in React round; component design with API contract.
- Blind 2023: rounds named JS coding, browser coding, system design.

## Razorpay (Glassdoor)
- Jul 2025: machine coding dynamic form from JSON; resume + basic JS/React.
- Jul 2024 Bengaluru: machine coding, system design, HM; "Implement Tabs like Material UI".
- Jun 2022: coding any framework; resume round on CI/CD, Docker, Jenkins.

## AI tools in interviews
- techinterview tracker (May 2026): AI-permitted: Anthropic, Cursor, Vercel, Replit, Glean, many YC startups. Prohibited: Meta, Apple, Amazon, Netflix, quant firms, banks. Verify with recruiter.
- GreatFrontEnd (Oct 2026) conflicts: Anthropic candidate guidance says no AI in live interviews unless told; Microsoft no outside help unless permitted; OpenAI varies. Canva has AI-assisted round (plan, build with AI at PR quality, discuss); Shopify allows tools; Google pilot with Gemini (May/Oct 2026); Meta AI round candidate-reported (CoderPad with assistant panel, bug fix -> feature -> optimize); LinkedIn AI round beside normal one (Feb 2026). Amazon: no gen AI unless permitted (Feb 2025).
- Judged on: breaking down ambiguity, selective AI use, validating output, debugging, PR quality code, explaining trade-offs. Canva says "AI showcase", "feature marathon", "hands-off" score badly.
- Review AI output for: state mutation, key={index}, eslint-disable exhaustive-deps, dangerouslySetInnerHTML with user data, debounce used to "fix" race conditions. Write failing test first.
- Rejections: hidden AI in no-AI round (proctoring catches paste/tab switch), uncritical acceptance, refusing AI entirely.

## ChatGPT-style chat frontend design (prachub, educative)
- Clarify: survive refresh? stop/regenerate/edit? context window overflow? markdown + code? Model = existing inference service.
- Cover: components, request/response contract, where history lives, context fitting, cancellation, failures before/during stream, TTFT, SSE vs WebSocket (traffic direction, proxies, auth, reconnect, SSE limits), long conversation rendering, scroll during stream.
- Techniques: stable shell vs streaming panel; explicit UI states not booleans; AbortController, cancel on new message mid-stream; buffer tokens per requestAnimationFrame; unclosed code fence state; never render model HTML, map to fixed component catalog with validated props; schema-validate structured output, fallback to text; handle moderation cut-off, partial output; TTFT > total time; aria-live polite without per-token announce.
- OpenAI: finals 4-6 hrs, 4-6 people; Feb 2026 coding: ChatGPT UI around a streaming function + new request mid-stream; design: internal Playground with model select, params, shareable presets.

## Frontend to AI engineer (GreatFrontEnd, Oct 2026)
- Job posts (Oct 2026): OpenAI Applied AI Eng Startups (5+ yrs, Python + JS); Anthropic Applied AI Eng Enterprise (4+ yrs, prompting, agents, evals, MCP); Ramp Applied AI Eng Fullstack (React/TS); Granola AI Eng (TS, React, Node, tracing, evals); LangChain Frontend Eng AI Observability (2+ yrs React/TS).
- Transferable: streaming, useChat status, Stop via AbortController, throttled UI updates, generic errors, OWASP LLM05 output handling. New: tool use (validate + gate), structured outputs, evals, retrieval, cost/latency (prompt caching), prompt injection OWASP LLM01.
- Order: backend basics -> LLM APIs + structured output -> tools + retrieval -> evals -> security -> observability.
