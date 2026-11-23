# Job market check for Ayush (Nov 2026)

Short answer: yes, there are jobs for your profile. Senior React/Next.js roles are still being posted in Delhi NCR, Bengaluru and remote. But plain frontend roles are fewer than before. The roles that are growing want frontend plus AI, or frontend plus some backend.

## 1. Are there jobs?

Indeed India search on 23 Nov 2026 (only searched, nothing applied):

- **Delhi NCR (Gurugram, Noida, Delhi):** a handful of good senior frontend roles. Best ones: CONXAI (Gurugram, React + TS + AI platform), Avya Technology (Noida, React/Next.js + AI tools), Ken Research (Gurugram). Many other results were MERN, .NET or low pay (one Next.js job paid Rs 12-15k a month).
- **Bengaluru:** more choice. NeoScript (Senior Frontend, React + Next.js, posted 6 Nov), AppsForBharat, Mercari India, VuNet, Electrolux, Metadesign (React Lead, posted 23 Nov).
- **Remote:** fewer pure frontend roles. Most remote senior roles want full stack (Node.js, Postgres) or are on US hours. Examples: Hire Hangar (Next.js + LLM, US hours), Mirantis (Next.js full stack, 8+ yrs), Mavvrik (AI native product engineer, 6-12 yrs, Claude Code, RAG, MCP).

Full list with links: [../jobs/shortlist.md](../jobs/shortlist.md)

## 2. What is the demand like?

- Frontend postings fell about 25% worldwide from Jan 2024 to Jan 2025, while full stack went up 9% (TalentNeuron, via LeadDev). React is still the main frontend skill.
- AI roles are growing fast in India. About 2.9 lakh AI job posts in 2025, expected 3.8 lakh in 2026 (Masai School). Agentic AI engineer demand up 260% in 2026 (CIEL HR, via Business Today). LLM engineer up about 86%.
- Developers with AI skills earn more. AI-focused developer roles were up 125% vs 2023 while non-AI roles fell 24% (TalentNeuron, global).

What this means for you: your React/Next.js depth is good and still in demand, but the best paid and growing roles now ask for "frontend + AI" or "product engineer" (frontend plus some backend plus AI).

## 3. Salary range (India, 5-8 years frontend)

From GreatFrontEnd's 2026 guide:
- Normal market: Rs 12-24 LPA
- Product companies and GCCs (global capability centers): Rs 18-40 LPA
- 8-12 years: Rs 20-35 LPA normal, Rs 32-60 LPA at product companies

With 6+ years, Next.js depth and some AI work, aim for product companies and GCCs, not service companies.

## 4. What to add (in order)

**A. Must add (shows up in most good job posts)**
1. **Show your AI work properly.** You already built a RAG assistant. Write one case study page for it: how it works, which model, how you chunk and search, how you test answers. Recruiters search for "RAG", "LLM", "AI SDK".
2. **Vercel AI SDK / OpenAI or Claude API with streaming and tool calling.** Build one small app: chat UI with streaming, tool calls, and structured output (Zod). This covers "generative UI" and "LLM integration" in job posts.
3. **Some backend: Node.js + PostgreSQL** (Supabase or Prisma is fine). Many remote senior roles reject pure frontend. Your BFF work is a good start, just show one project with a real database.
4. **Testing: Playwright end to end.** You have Jest/RTL. Playwright shows up in almost every senior post now.

**B. Good to add**
5. **Auth in Next.js:** Auth.js / OIDC / JWT sessions. You used Auth.js in Partner Studio, so add it to the resume skills list.
6. **Design system work:** Storybook, Radix or shadcn/ui. Many senior roles ask for "own the component library".
7. **Monorepo tools:** Turborepo, pnpm workspaces.
8. **Monitoring:** Sentry, PostHog, feature flags.
9. **MCP / agents basics:** a small MCP server or an agent that uses tools. Newer AI product roles (like Mavvrik) ask for it.

**C. Profile fixes**
- Make the resume say "Senior Frontend Engineer (React, Next.js, AI)" at the top so it matches AI-frontend searches.
- Fix the 3+ vs 4+ years at FITPASS mismatch.
- Put numbers on Lighthouse and Core Web Vitals wins if you have them.
- GitHub: most public repos are learning repos (DSA, JavaScript practice). Pin 2-3 strong projects with a README and live link, like the AI assistant and a Next.js app.
- LinkedIn headline should match the resume.

## Sources

- https://www.greatfrontend.com/blog/frontend-developer-salary-india
- https://www.masaischool.com/blog/the-ai-skills-indian-employers-are-actually-hiring-for-in-2026/
- https://www.businesstoday.in/jobs/story/ai-job-shift-agentic-ai-engineers-emerge-as-the-hottest-tech-hire-demand-up-260-percent-553968-2026-09-08
- https://leaddev.com/ai/does-ai-spell-death-front-end-engineering
- Indeed India job search, 23 Nov 2026
