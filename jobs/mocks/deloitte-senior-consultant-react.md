# Mock interview: Deloitte, Senior Consultant React JS (Delhi)

Job: https://to.indeed.com/aaj4m6bz72vw (posted 19 Nov 2026, 5+ yrs)
Made: 26 Nov 2026. Sample of the per-job mock format from [plan/job-dashboard-plan.md](../../plan/job-dashboard-plan.md) section 4.

## What we know about Deloitte frontend interviews (public reviews)

- Bengaluru Senior Consultant, Apr 2026: one round of "opinion-heavy React questions", rejected. Asked: other ways to handle form submit besides onClick/onSubmit; React vs Angular components and why; how you handle modal/accordion/dropdown state; event bubbling and how to stop it. (Glassdoor)
- Hyderabad Full Stack, Mar 2026: online test, 3 technical rounds, HR. React, Node, problem solving. Asked to design a rate limiter, show a demo video of a project, and build something using AI. (Glassdoor)
- Senior Consultant posts 2023-24: React lifecycle and hooks, useEffect dependency array, is JS single-threaded and how async calls work, map vs forEach, hoisting, scope, live coding on arrays/strings (most repeated item), then a round on performance/security/best practices, then HR. (Board Infinity forum)

Sources in [research/raw/2026-11-26-indeed-search.md](../../research/raw/2026-11-26-indeed-search.md).

**Expected rounds:** (1) online test or first technical, JS + React basics and live coding, (2) technical deep dive: performance, security, architecture, your projects, (3) manager / client-fit talk, (4) HR and salary.

Key lesson from the rejected candidate: for "opinion" questions, give your choice AND the reason AND when you would choose the other option. Do not just list facts.

---

## Round 1: JS + React basics, live coding

**Q1. JavaScript is single-threaded. So how does a fetch call not block the page?**
- Must cover: call stack, Web APIs do the waiting, callback/microtask queue, event loop picks from queue when stack is empty. Promises go in the microtask queue, run before setTimeout.
- Trap: saying "JS uses multiple threads for async".
- Follow-up: order of output for `setTimeout(0)`, `Promise.resolve().then`, and a plain `console.log`.

**Q2. useEffect dependency array: what happens with no array, empty array, and [a, b]?**
- Must cover: every render / once after mount / when a or b changes (by Object.is). Cleanup runs before next effect and on unmount. Strict Mode runs it twice in dev.
- Trap: putting an object or function made during render in the array, which re-runs every time.
- Follow-up: "Would you fetch data in useEffect in a Next.js app?" Answer from FITPASS: no, use Server Components for first load and TanStack Query for client refetch. Say why.

**Q3. Live coding: find the most repeated item in an array.**
- Must cover: one pass with a Map of counts, track max while counting. O(n) time, O(k) space. Handle ties and empty array.
- Follow-up: top 3 most repeated (sort entries, or a small heap).

**Q4. map vs forEach. And hoisting with var / let / function.**
- Must cover: map returns a new array, forEach returns undefined. var is hoisted as undefined, let/const are in the temporal dead zone, function declarations are fully hoisted.

**Q5. Event bubbling: what is it, how do you stop it, when would you NOT stop it?**
- Must cover: event goes target to parents; `stopPropagation()`; event delegation relies on bubbling, so stopping it can break analytics or outside-click handlers.
- Follow-up: capture phase, and how React attaches events at the root.

## Round 2: technical deep dive (opinion and design)

**Q6. Other than onClick and onSubmit, how can you handle a form submission?**
- Must cover: native form with `action` (Server Actions in Next.js, what Ayush used at FITPASS with `{ ok, message }` results), `useActionState`, keyboard Enter submit, form libraries (React Hook Form) and why: less re-render, validation with Zod.
- Give an opinion: "For server writes in Next.js I prefer Server Actions because ... For a big client-only form I use React Hook Form because ..."

**Q7. How do you manage state for modal, accordion and dropdown across an app?**
- Must cover: local useState first; lift up only when siblings need it; URL state for things that should survive refresh or share (e.g. open tab); a small Zustand store for global UI like one-modal-at-a-time. Accessibility: focus trap, Esc to close, aria-expanded.
- Trap: "Put everything in Redux".

**Q8. React vs Angular components: how are they different and why?**
- Must cover: React = functions + hooks, one-way data flow, JSX, you pick the libraries. Angular = classes with decorators, DI, templates, two-way binding, full framework. Why: different goals (library vs batteries-included). When you would pick each (big enterprise team wanting one standard way = Angular can make sense).

**Q9. A page on a client project is slow. Walk me through what you do.**
- Must cover: measure first (Lighthouse, Web Vitals, React Profiler), then fix by cause: LCP (preload hero image with fetchPriority, as at FITPASS), CLS (reserved aspect ratios), INP (split long tasks, memo only where profiler shows), bundle (next/dynamic below the fold). Say the numbers you got.

**Q10. Design a rate limiter for a web app.**
- Must cover: where (edge/API layer), key (IP or user), algorithm (fixed window vs sliding window vs token bucket, and trade-offs), store (Redis so all servers share counts), response 429 with Retry-After. Ayush's real example: Upstash Redis rate limit on his portfolio AI chat.

**Q11. Security basics on the frontend.**
- Must cover: XSS (React escapes by default, danger in dangerouslySetInnerHTML), tokens in httpOnly cookies not localStorage, CSRF with sameSite cookies, check auth on the server not only in middleware (CVE-2025-29927).

## Round 3: manager / client fit

**Q12. Tell me about a project you are proud of.** Use STAR with Partner Studio (20+ corporate clients) or the Nutrition Dashboard (60k+ users). Have one number ready for result.

**Q13. A client changes requirements late in the sprint. What do you do?** Show calm trade-off thinking: impact, options, tell the PM/client early, agree what moves out.

**Q14. Why Deloitte, and why leave FITPASS now?** Positive: variety of client problems, bigger scale, learning across domains. Never criticise the current company.

**Q15. Show a project you built with AI.** Ready: portfolio RAG assistant (routing before model, Upstash Vector). Keep a 2-minute demo.

## Questions Ayush can ask them
1. Which client domains would this role work with first?
2. Is the team building new products or maintaining existing ones?
3. How do you measure success for a senior consultant in the first 6 months?
4. Is there room to work on AI/GenAI frontend projects?

## How we practise
Ayush answers Q1-Q15 here in the chat (typing is fine). Claude asks follow-ups and scores each 1-5 on: correct, explains why, trade-offs, clear, real example. Weak ones go to a fix list.
