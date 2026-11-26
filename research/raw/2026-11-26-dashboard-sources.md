# Raw notes: dashboard plan research (26 Nov 2026)

Searches run: Next.js 16 auth guidance, CVE-2025-29927, Upstash Redis free tier, ATS match rate data.

## Pages read
1. https://upstash.com/pricing/redis.md
   - Free: 1 database, 250 MB data, 10 GB bandwidth, "500K commands per month" (FAQ). No SLA, no IP allowlist, no encryption at rest on free.
2. https://www.jobscan.co/blog/what-jobscan-match-rate-should-i-aim-for/
   - Recommends 80% match rate as "sweet spot", 75% still competitive. Warns against keyword stuffing / hidden white text. No interview-rate vs score data. Vendor blog.
3. https://arc.dev/employer-blog/nextjs-app-router-authentication/
   - proxy.ts (Next.js 16) = optimistic redirects only, "shouldn't be your only line of defense".
   - Real checks in Server Components, Route Handlers, Server Actions, data access layer (requireUser() helper). Client guards are not security.
   - Cookie: httpOnly, secure, sameSite lax, path /, maxAge. Never localStorage.
   - Uses jose for JWT verify. Recommends Better Auth for new apps, keep Auth.js v5 for existing. Lucia deprecated.
   - Cites CVE-2025-29927 patched versions 12.3.5, 13.5.9, 14.2.25, 15.2.3.
4. https://vercel.com/changelog/vercel-firewall-proactively-protects-against-vulnerability-with-middleware
   - CVE-2025-29927: bypass authorization in Middleware via x-middleware-subrequest header. Vercel-hosted apps were not affected, still update.
5. https://scale.jobs/blog/ats-scores-matter-real-job-search-data
   - Only number: "only 4-6 out of every 250 resumes" lead to interview (no source). Calls 75-85% score ideal, <60% major issues (no data). Marketing page.

## Other search results seen (not read in full)
- https://vercel.com/kb/guide/application-authentication-on-vercel
- https://clerk.com/articles/nextjs-authentication-guide-2026
- https://auth0.com/blog/handling-auth-nextjs16-with-server-actions-middleware/
- https://nvd.nist.gov/vuln/detail/CVE-2025-29927
- https://www.jobscan.co/blog/ats-resume/

## Facts reused from this repo
- Portfolio stack (research/raw/2026-11-23-portfolio-full-read.md): Next.js 16, TS, AI SDK v7, Gemini, Upstash Vector, Upstash Redis rate limit, Tailwind 4, Vitest. Vercel functions.
- Ayush used Auth.js v5 Credentials + proxy.js session check at FITPASS Partner Studio.
- Company interview data: jobs/companies/*.md. Reject reasons: research/other-candidates-2026.md.

## My own judgment (not from a source)
- Chance-% base rates by channel (cold 5%, careers page 7%, referral 20%, recruiter 30%) and multipliers are my starting guesses. Must be calibrated with Ayush's real results.
- Job JSON size estimate 20-50 KB.
