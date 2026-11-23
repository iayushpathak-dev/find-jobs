# Raw notes: interviews at AI companies / AI startups, frontend + AI roles (read 23 Nov 2026)

Mostly aggregators and prep vendors, few first-person posts. Treat as likely questions.

## ombharatiya/FAANG-Coding-Interview-Questions AI-Companies file (GitHub, Nov 2026, aggregated from Reddit/Blind/Glassdoor; only first third read)
- xAI: 4 hr take-home (improve X search via Grok API, semantic), repo + 5-6 min demo video in 24 hr, AI allowed. Onsite 60 min no-AI: extend 70-100 line class (token queue, rate limiter, TTL KV, batching, LRU). Frontend (Sep 2026): React typeahead with async suggestions, keyboard nav, stale-result/race handling, no libs.
- Mistral: screen 60 min; take-home 4-8 h small LLM/agent experiment written like a paper; LLM quiz; RAG/agent build defending retrieval, latency, evals.
- Cohere: AI-enabled coding: agent loop with tool-call parsing; token rate limiter; batch aggregator (32 items or 50 ms); streaming response parser; RAG failure modes; NDCG/MRR/recall@k. Marked down for leaning on AI.
- Perplexity: OA 75-90 min; credit tracker, time-versioned KV, in-memory FS; RAG with citations (chunking, BM25 vs dense vs hybrid, rerank), hallucination mitigation; design long-running query service (submit, poll, streamed partial results, cancel, retry). 11-23 days.
- Scale AI: CSV-to-JSON service calling classification + embedding APIs; debug pipeline where hashing inflates token cost; design insurance-claims agent (RAG, routing, token cost).
- Cursor: apply streaming LLM edits as tokens arrive; multi-file diff tracking; context retrieval for prompts; rope text buffer; tab prediction under 100 ms; onsite build a feature in real codebase (paid). Raw unreviewed AI output = fast reject.
- Meta AI-enabled round: 60 min CoderPad + AI panel: bug fix -> 120+ line feature -> optimize. Rubric: problem solving, code quality, verification, communication.

## OpenAI Frontend (DesignGurus Sep 2026 + GreatFrontEnd guide)
- Rounds: recruiter, coding screen (React/TS UI), frontend system design, debugging/refactor, project presentation, behavioral. Finals 4-6 hrs, 4-6 people, 1-2 days.
- Candidate tasks: Feb 2026 ChatGPT-style UI on a supplied chunked-streaming function; match reference video layout; handle extra requests mid-response; show one char at a time. Aug 2025 GPU-credit grants/deductions/expiry/balance over time. Dec 2025-Feb 2026: separate streamed display from incoming chunks; toasts with manual + timed dismiss; template autocomplete in rich text editor. Jun 2026: why your React code works; DOM/CSS text rendering. Calendar day/week/month with paginated data.
- Design: internal Playground (model select, params, chat, shareable presets: API, schema, component tree, real-time, concurrent edits; loading a preset while a response streams). ChatGPT conversation, canvas editor with collaborators.
- Also: debounce without library; why component renders twice; CORS; typewriter effect.
- Tips: separate request state / buffered data / displayed text; cancellation on unmount, mid-stream edit, navigation; write one test; prepare backend half too.

## Distyl Senior+ AI Engineer (PracHub, May 2026)
- Take-home ~4 h, AI allowed: convert Whisper pipeline from full transcript to chunked streaming; multi-speaker; speed.
- Design: streaming LLM chatbot that switches model when token count exceeds rate limit; streaming behind load balancer; when to write chat history to DB. 20 of 45 min on own project.
- Deep dive: deploy, shared platform vs per-customer, versioning.

## ResortPass Senior Frontend (FrontendLead, 10+ yrs)
- LeetCode Decode String; critique React snippets; Next.js filtering with client vs server state synced to query params.

## Guibai / Juejin frontend AI primer (Aug 2026)
- Topics: tokens, context, temperature, embeddings, RAG hybrid search, ReAct + function calling, MCP, SSE typewriter, sanitized markdown (react-markdown + DOMPurify), prompt injection, BFF key proxy, WebLLM, Transformers.js. Cap agent iterations; batch tokens.

## gitGood AI startup interview (Jun 2026, advice)
- Loop: screen, take-home 4-8 h (AI feature), review, live coding (SDK, function calling, structured output, simple eval), system design (RAG, agent platform, eval pipeline), founder chat.
- Take-homes: RAG with recall + answer eval; task agent with success rate; eval framework.
- Signals: shipped AI features, eval reasoning, cost/latency awareness, right-sized complexity, product taste, velocity.
- Tips: README with trade-offs + eval suite; report cost per request + p50/p95 latency; "what I'd do with more time"; 3-5 AI stories with numbers.
- US pay estimates (unsourced): Series A senior $180-250K base, frontier labs $300-500K+.

## OnlyFrontendJobs frontend questions 2026 (Swiggy, Flipkart, Zepto, startups)
- Q: design real-time AI chat UI (route -> LLM, SSE, useChat, batch tokens ~50 ms, error boundary, optimistic user msg); never LLM keys on client; avoid INP drop while streaming (throttle, ref then commit).
- Others: useTransition/useDeferredValue, React 19 useActionState, hydration mismatch, CWV, SSR/SSG/ISR, virtualized list, ARIA, userEvent tests.
- Pay (base, from LeetCode/Levels.fyi per page): Swiggy senior 5-8 yrs Rs 40-55L, staff Rs 55-90L; Razorpay senior Rs 27-45L, staff Rs 45-65L.
