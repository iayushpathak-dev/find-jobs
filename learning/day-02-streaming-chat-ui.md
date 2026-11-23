# Day 2 (Tue 25 Nov): Next.js mein streaming chat UI (JobMatch AI ka pehla screen)

Aaj ka goal: kal ka terminal chatbot ab browser mein. Text type hota dikhe, Stop button, loading, error + Retry.
Time: ~3 ghante. Docs version: AI SDK v7 (`ai`, `@ai-sdk/react`).

---

## Part A: Samjho (15 min)

### Pura flow ek line mein

```
Browser (useChat)  --POST /api/chat (messages)-->  Next.js Route Handler (streamText)  -->  LLM
Browser  <--  stream (tukde tukde)  --  Route Handler  <--  tokens  --  LLM
```

Restaurant waala example:
- **Browser = customer.** Order deta hai (message).
- **Route Handler = waiter.** Order kitchen tak le jaata hai. Waiter ke paas hi "kitchen ki chabi" (API key) hai, customer ke paas nahi.
- **LLM = kitchen.** Khana ek-ek plate karke bhejti hai, waiter turant table par rakhta jaata hai (streaming).

Isliye API key kabhi browser mein nahi jaati. Ye kal ka interview sawal #5 ka jawab hai.

### Do tarah ke messages (interview mein poochte hain)

| | UIMessage | ModelMessage |
|---|---|---|
| Kahan | Browser / React state | LLM ko jaata hai |
| Shape | `{ id, role, parts: [...] }` | `{ role, content }` |
| Kyun | UI ko id, tool cards, metadata chahiye | Model ko sirf text/tool data chahiye |

Server par `convertToModelMessages(messages)` UI waale ko model waale mein badalta hai.

### `parts` kya hai

Ek AI message mein sirf text nahi hota. Usme text, reasoning, tool call, tool result sab ho sakte hain, ek order mein. Isliye `message.parts.map(...)` karke render karte hain, `message.content` nahi. Day 4 mein isi se tool cards (generative UI) banayenge.

### `status` ke 4 states (UX yahin banta hai)

- `submitted`: request gayi, pehla token abhi nahi aaya -> spinner / "thinking..."
- `streaming`: text aa raha hai -> Stop button dikhao
- `ready`: sab aa gaya -> input enable
- `error`: kuch fail hua -> generic message + Retry

> Interview line: "I drive the chat UI from one status value: submitted, streaming, ready, error. That gives me spinner, stop, input lock and retry without extra state."

---

## Part B: Setup (15 min)

```bash
pnpm create next-app@latest jobmatch-ai   # App Router: Yes, Tailwind: Yes, TypeScript: Yes
cd jobmatch-ai
pnpm add ai @ai-sdk/react zod
echo "AI_GATEWAY_API_KEY=yahan_apni_key" > .env.local
```

`.env.local` Next.js ke default `.gitignore` mein already hai. Fir bhi `git status` se check kar lena.

Ye `jobmatch-ai` hi aage 12 din ka project hai. GitHub par public repo bana do aaj hi.

---

## Part C: Code

### Step 1: Server route (`app/api/chat/route.ts`)

```ts
import {
  convertToModelMessages,
  createUIMessageStreamResponse,
  streamText,
  toUIMessageStream,
  type UIMessage,
} from 'ai';

export const maxDuration = 30; // Vercel par 30 sec tak stream chal sake

export async function POST(req: Request) {
  const { messages }: { messages: UIMessage[] } = await req.json();

  const result = streamText({
    model: 'anthropic/claude-sonnet-5.5',
    instructions:
      'You are JobMatch AI. You help a senior frontend engineer compare job descriptions with their profile. Be short and specific.',
    messages: await convertToModelMessages(messages),
    temperature: 0.3,
  });

  return createUIMessageStreamResponse({
    stream: toUIMessageStream({ stream: result.stream }),
  });
}
```

### Step 2: Chat page (`app/page.tsx`)

```tsx
'use client';

import { useChat } from '@ai-sdk/react';
import { useState } from 'react';

export default function Chat() {
  const [input, setInput] = useState('');
  const { messages, sendMessage, status, stop, error, regenerate } = useChat(); // default: POST /api/chat

  const busy = status === 'submitted' || status === 'streaming';

  return (
    <main className="mx-auto flex min-h-screen max-w-2xl flex-col gap-4 p-4">
      <h1 className="text-xl font-semibold">JobMatch AI</h1>

      <ul className="flex flex-1 flex-col gap-3" aria-live="polite">
        {messages.map(m => (
          <li key={m.id} className={m.role === 'user' ? 'self-end rounded bg-blue-600 p-3 text-white' : 'rounded bg-zinc-100 p-3 dark:bg-zinc-800'}>
            {m.parts.map((part, i) =>
              part.type === 'text' ? <p key={i} className="whitespace-pre-wrap">{part.text}</p> : null,
            )}
          </li>
        ))}
        {status === 'submitted' && <li className="text-sm text-zinc-500">Thinking...</li>}
      </ul>

      {error && (
        <div role="alert" className="flex items-center gap-2 text-red-600">
          Something went wrong.
          <button onClick={() => regenerate()} className="underline">Retry</button>
        </div>
      )}

      <form
        className="flex gap-2"
        onSubmit={e => {
          e.preventDefault();
          if (!input.trim()) return;
          sendMessage({ text: input });
          setInput('');
        }}
      >
        <textarea
          value={input}
          onChange={e => setInput(e.target.value)}
          placeholder="Paste a job description or ask something..."
          className="flex-1 rounded border p-2"
          rows={3}
          disabled={busy}
        />
        {busy ? (
          <button type="button" onClick={() => stop()} className="rounded border px-4">Stop</button>
        ) : (
          <button type="submit" className="rounded bg-black px-4 text-white">Send</button>
        )}
      </form>
    </main>
  );
}
```

Chalao: `pnpm dev`, kholo http://localhost:3000. Ek lamba JD paste karke poocho "Is this a good fit for a React/Next.js dev with 6 years?"

### Step 3: Network tab mein dekho (sabse important 5 min)

DevTools > Network > `chat` request > Response. Tumhe chunks aate dikhenge. Ye hai asli streaming. Interview mein bolna ki tumne ye debug kiya hai, bahut accha impression padta hai.

---

## Part D: Khud karo

1. **Markdown:** AI ke jawab mein `**bold**` aur lists aate hain. `react-markdown` laga ke sirf assistant messages ko markdown render karo.
2. **Auto scroll:** naya token aaye to list neeche scroll ho, par agar user ne upar scroll kiya hai to mat karo. (Ye senior level detail hai, interviewers poochte hain.)
3. **Enter = send, Shift+Enter = new line** textarea mein.
4. **Error test:** `.env.local` mein key galat karo, error UI dikhna chahiye, server ka asli error user ko nahi.
5. **Commit + push** `jobmatch-ai` repo mein. README mein 2 line: kya hai, kaise chalana hai.

---

## Part E: Interview sawal

1. `useChat` ke `status` ki 4 values kya hain, har ek par UI mein kya dikhaoge?
2. UIMessage aur ModelMessage mein farak? Convert kyun karna padta hai?
3. API key server par kyun? Agar kisi ne tumhara `/api/chat` route spam kiya to? (Hint: Day 9, rate limit + auth.)
4. Streaming ke time auto-scroll aur "user ne upar scroll kiya" ko kaise handle karoge?
5. 500 messages ki chat slow ho gayi. Kya karoge? (Hint: virtualization, purane messages model ko summarize karke bhejna.)

---

**Kal (Day 3):** JD paste karo -> AI se **typed JSON** nikalo (skills, years, must-have, nice-to-have) Zod schema ke saath, aur usko UI mein card ki tarah dikhao.
