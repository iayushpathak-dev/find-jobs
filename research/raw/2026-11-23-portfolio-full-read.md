# Raw notes: full read of ayushpathak.co.in (23 Nov 2026)

Pages read: homepage, /resume, /projects, /experience, /blog, /projects/fitpass-corporate-pwa, /projects/backend-for-frontend, /projects/fitpass-website-rendering, /projects/nutrition-dashboard, /projects/liveness-verification, /projects/ai-portfolio-assistant. Paraphrased, numbers exact.

## Blog
No posts. /blog lists planned topics only: React Internals and Rendering; Next.js Rendering and Caching; TypeScript Patterns for Frontend Apps; Frontend System Design; Performance Optimization in Production React Apps; State Management (Redux, Zustand, React Query); Debugging Production Applications. Labels planned: Professional Experience, Hands-on Implementation, Experiment, Learning Notes.

## Career
- FITPASS, Senior Frontend Engineer, Nov 2022 to now ("4+ years"; homepage stats still say "3+ years at FITPASS"). JS, React, Next.js (Pages + App Router), Zustand, React Query, Tailwind, MUI. Mentors 2 juniors.
- Elite Mindz, Feb-Nov 2022: QTickets multi-region booking (movies, events, sports), seat selection, checkout, REST, Doha Bank payment gateway. No case study, no metrics.
- Enbake, Mar-Dec 2021: LOGITRACK IoT live shipment dashboard (React, TS, REST). No case study, no metrics.
- Magic Software, Jan 2020-Feb 2021: EdTech modules in React + HTML5, Flash migration, accessibility. No metrics.
- Resume highlights: "6+" years; "20+" corporate clients on Partners Studio; "60,000+" users Nutrition Dashboard; "4" rendering modes (SSR, SSG, ISR, CSR). Last updated Aug 2026.
- Resume skills also: TensorFlow, Face Landmarks Detection, Redux, Zustand, WCAG 2.1 AA, Jest, RTL, Claude Code, Codex, ChatGPT.
- Resume FITPASS bullets: webhook-triggered ISR; "FITSHOP: rebuilt the membership platform on the App Router using Server Components and Server Actions" (Fitshop page calls it an e-commerce store, wording differs); Aghora integration (dietitian chat, scheduled calls, audio calls, chat history migration).

## Partner Studio (fitpass-corporate-pwa)
- Problem: corporate/insurance partners give FITPASS to users who should not need another app. Web app inside partner WebViews or browser. Signed partner link logs user in, scoped to partner.
- Challenge: one codebase, 20+ partners with own entry route, branding, features; old Android/iOS WebViews; fitness bookings, healthcare, face checks, payments.
- Features: studio search/details, reviews, schedule, bookings, favourites, QR check-in, "Show your pass"; Fitheal doctor consults, health checkups, slot booking, EHR, quizzes, HRA; face liveness + QR check-in, face-scan health report with vitals; membership upgrade (plans, coupons, checkout, payment, invoices); profile edit with OTP.
- Architecture: Auth.js v5 Credentials provider set up in a route handler on the partner link; backend token + partner details in encrypted httpOnly JWT cookie; proxy.js checks session on every route (redirect to not-authorized, 401 for APIs); /order/[corporate_name] must match user's partner else 404.
- Three data paths: Server Components for page-open reads; Server Actions for writes ({ ok, message }); TanStack Query via BFF (/api/service allowlist) for load-more, search, filters. Partner headers built on server from session.
- Zustand per-request store provider; flow state in httpOnly cookies not localStorage; backend 412 opens shared precondition screen; backend HTML sanitised.
- WebView UI: 100dvh, safe-area padding, iOS keyboard via visualViewport, 16px inputs, reduced motion. Targets Chrome 88+, iOS Safari 14+.
- Ops: health endpoint for K8s probes (no backend call); multi-stage non-root Docker; one image all envs via runtime env; written security review with severity + owner.
- Stack: Next.js 16, React 19, Auth.js v5, TanStack Query, Zustand, Tailwind 4, TF.js + MediaPipe, Docker. JavaScript (team choice).
- Impact: 20+ partners. No perf numbers. Limitation: some screens use static data until APIs ready.

## BFF (backend-for-frontend)
- Problem: website + partner apps call old PHP APIs, newer services, gRPC, third-party APIs; responses carry extra fields.
- Service map "200+" entries; browser sends service name + params to /api/service; map resolves URL, method, content type, headers (guest, logged-in, Fitshop, corporate).
- Legacy responses filtered on server. Per-corporate UI config merged on top of API data.
- Third-party routes: geocoding, place details, IP lookup, reCAPTCHA verify, face scan, uploads; keys on server; responses reshaped.
- gRPC events: /api/grpc-service -> GeneralEvent.SendGeneralEvent; event in protobuf Any; client built from .proto at runtime; protos bundled into standalone build.
- Stack: Route Handlers, JS, @grpc/grpc-js, proto-loader, REST.
- Trade-offs listed: BFF in Next.js vs separate service; filter in BFF vs fix backend; extra hop.
- Homepage card shows "100" Lighthouse SEO. No latency/caching numbers.

## FITPASS website (fitpass-website-rendering)
- fitpass.co.in, main acquisition channel, thousands of studio/city/activity pages. "200+" routes, App Router route groups (common, corporate/partner, partner network, Fitshop).
- Studio/city/listing pages SSR per request (location cookies, user, changing data). 4 modes per resume.
- SEO: generateMetadata from backend meta (title, description, canonical, OG, Twitter); geo meta on studio pages; JSON-LD; sitemap via rewrites; catch-all route resolves city/filtered listings, follows API 301/302/404; noindex outside prod.
- Perf: device-specific LCP preload with fetchPriority high; reserved aspect ratios; next/font swap; next/dynamic below fold; CDN images.
- PageSpeed Insights homepage, 23 Nov 2026: CWV passed mobile + desktop (CrUX 28 days). Mobile LCP 1.6 s, INP 110 ms, CLS 0. Desktop LCP 1.3 s, INP 69 ms, CLS 0. Lighthouse SEO 100, Best Practices 100, Accessibility 96. Lesson: lab vs field disagree; throttled mobile Lighthouse flags JS + third-party.
- Analytics: one helper -> GA4, Meta Pixel, Segment; UTM + gclid captured in proxy; server-side Meta Conversions API with hashed data.
- Deploy: standalone build behind nginx + supervisor on Kubernetes; health check holds nginx until Next ready; outputFileTracingIncludes for protos.

## Nutrition Dashboard
- "~50 routes", "20+" dietitians, "60,000+" users.
- Problem: dietitians need member health answers, diet plans, food library, follow-ups across ~50 screens without dev per screen.
- JSON config -> schema (columns, labels, formats, actions, filters) -> single renderer: table with CRUD, server pagination, filters, search. Feature flags true/false.
- Workflows: HRA follow-up + diet plan on same screen; reusable plans by reference ID assigned by keyword; allergy-aware diets; food library with images/calories; renewal payment links.
- Trade-offs: config vs hand-built (edge cases move into renderer); broken config breaks screen so validate on load; templates vs custom diets.

## Liveness Verification + QR Attendance
- Problem: QR check-in at gyms; backend may require face check to stop shared memberships; verified profile photo; must run in partner WebViews on any phone.
- Challenges: low-end Android, GPUs (Adreno 8xx break GPU model); paid Luxand call must not get blurry/dark/empty photos; check sits in 5 flows and must return to original action.
- TF Face Landmarks Detection on MediaPipe runtime (refined landmarks, up to 2 faces), prewarmed. GPU detect via WebGL; known-bad GPUs -> MediaPipe Tasks FaceLandmarker on CPU with blink from blendshapes; ?face_cpu= flag.
- Frame grading every 250 ms: oval position, distance, yaw, eyes open, brightness, sharpness (variance of Laplacian on fixed grayscale crop).
- Second-face guard with BlazeFace short-range; counts after 3 consecutive frames.
- Strict thresholds first 10 s then relaxed; 30 s timeout; auto-capture after 3 passing frames, sharpest kept. Loop reschedules itself instead of setInterval.
- Crop, compress (lower JPEG quality then size to fit limit). Local gate: exactly one sharp face before paid call. Luxand verdict normalised pass/fail/unknown. Upload: 200 replays saved request; 409, 410, 400 retry; max 2 retries.
- html5-qrcode one scan per open; 403 -> face check; time-stamped QR pass; same component in 5 flows (booking, QR check-in, profile photo, onboarding photo, device replacement); useDeviceCheck one-device rule. ?face_debug=1; Segment tracking each step.
- Trade-offs: in-browser vs server detection; landmarks vs dedicated liveness; relaxed thresholds. No metrics on page.

## AI Portfolio Assistant (RAG + web search), 2026
- /assistant; answers from published portfolio content with sources; Google Search only for current tech questions. Code: github.com/iayushpathak-dev/common-portfolio.
- /api/chat: Zod validation, rate limit, route by scope + intent. Out-of-scope/injection -> fixed reply, no model call. Personal/technical -> Gemini embeddings -> Upstash Vector (published only, top-K, similarity threshold) -> grounded streamed answer with links; nothing relevant -> "I don't have that information". Current tech -> model with Google Search grounding.
- Ingestion: typed content files with publish status; POST /api/rag/reindex (secret): chunk, diff by content hash, embed changed only, upsert, delete obsolete. Safe every deploy.
- Decisions: RAG vs all data in prompt (v1 did that); app-level routing before model; personal never uses web search; Upstash Vector over pgvector/Vectorize (REST from Vercel functions, no pooling, free tier); keyword router over LLM classifier.
- Limitations: threshold/chunking still tuning; router can misclassify; injection risk reduced not eliminated; free tier quotas.
- Stack: Next.js 16, TypeScript, AI SDK v7, Gemini/Gemma, Gemini embeddings, Upstash Vector, Upstash Redis rate limit, Tailwind 4, Vitest.
- Not on site: exact model names, embedding dim, chunk size/overlap, top-K, threshold, eval results.

## Other project pages (not read yet)
/projects/fitshop, /projects/fitfeast-webview (Agora chat + RTC), /projects/configurable-corporate-journeys ("all 20 partner funnels"), /projects/marketing-landing-pages, /projects/feedback-solution, /projects/native-app-webview-integration (~30 screens under /app/*), /projects/abdm-abha-integration (ABHA via Aadhaar OTP), /projects/claude-code-workflow, /about.
