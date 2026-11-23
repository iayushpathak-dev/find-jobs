# Day 1 (Mon 24 Nov): LLM basics + pehla AI program

Aaj ka goal: samajhna ki LLM andar se kaise "sochta" hai, aur terminal mein apna chhota chatbot chalana.
Time: ~2.5 ghante (30 min padhna, 2 ghante code).

---

## Part A: 6 cheezein jo har AI interview mein aati hain

### 1. LLM kya hai? (phone ka autocomplete, bas bahut bada)

Phone keyboard mein "Good" likho to wo "morning" suggest karta hai. LLM bhi yahi karta hai: **agla word guess karna**. Bas usne itna saara internet padha hai ki guess bahut accha ho gaya hai.

Ek word guess kiya, usse jod diya, phir agla guess kiya... aise poora jawab banta hai. Isliye ChatGPT/Claude mein text ek-ek karke aata dikhta hai.

> Interview line: "An LLM predicts the next token again and again, based on everything before it."

### 2. Token (AI ka "paisa" aur "unit")

LLM words nahi padhta, **tokens** padhta hai. Token = word ka tukda.
- "running" = shayad 1 token, "unbelievable" = 2-3 tokens
- Rough hisaab: **1 token ~ 4 English characters ~ 0.75 word**. Hindi/Hinglish mein tokens zyada lagte hain.

Kyun important hai:
- **Bill tokens par banta hai.** Input tokens (jo tum bhejte ho) + output tokens (jo model likhta hai). Output aam taur par mehenga hota hai.
- Frontend engineer ke liye matlab: chat history bina soche har baar poori bhejoge to bill aur speed dono kharab.

### 3. Context window (model ki "short term memory")

Ek request mein model maximum kitne tokens dekh sakta hai, wo uska context window hai. Jaise exam mein ek A4 sheet cheat sheet: jo sheet par hai wahi yaad hai, baaki kuch nahi.

**Sabse badi baat: LLM ko pichli baat yaad nahi rehti.** Har request naya hota hai. "Memory" ka illusion hum banate hain: har baar poori chat history (`messages` array) dobara bhejte hain. Aaj ke code mein ye khud dekhoge.

### 4. Messages aur roles

Har request ek array hota hai, jaise React mein state ka array:

```ts
[
  { role: 'system', content: 'Tum ek helpful career coach ho. Short jawab do.' }, // rules
  { role: 'user', content: 'Mera naam Ayush hai' },
  { role: 'assistant', content: 'Hi Ayush!' },
  { role: 'user', content: 'Mera naam kya hai?' }, // model ko yaad hai kyunki history bheji
]
```

- **system** = boss ke rules (tone, kya karna hai, kya nahi). AI SDK v7 mein isko `instructions` bolte hain.
- **user** = user ne kya bola
- **assistant** = model ne pehle kya bola

### 5. Temperature (creativity ka knob)

- `0` ke paas = har baar lagbhag same, seedha jawab. Use: data nikalna, JSON, classification.
- `1` ke paas = zyada creative, har baar alag. Use: ideas, marketing text.

Is project mein zyada jagah low temperature chahiye, kyunki hum resume vs JD match kar rahe hain, kahani nahi likh rahe.

### 6. Streaming (UX ka asli game)

Bina streaming: user 8 second blank screen dekhega, phir poora jawab ek saath.
Streaming ke saath: 0.5 second mein pehla word aa jata hai, baaki type hota dikhta hai.

Ye **frontend engineer ka sabse bada plus point hai** AI teams mein. Backend waale model call kar lete hain, par smooth streaming UI, loading state, stop button, error retry, ye tum best karoge.

> Interview line: "Streaming does not make the model faster. It cuts the time to the first word, so the app feels fast."

### Bonus: Hallucination

Model confident hokar galat bol sakta hai, kyunki wo "sach" nahi, "agla likely word" nikal raha hai. Fix: model ko sahi data do (RAG, Day 6-7), aur tools do (Day 4). Ye line yaad rakho, har AI interview mein poochte hain.

---

## Part B: Setup (20 min)

1. Node 22+ check karo: `node -v`
2. pnpm na ho to: `npm i -g pnpm`
3. API key: **Vercel AI Gateway** key banao (vercel.com par login, AI Gateway section, "Create API key"). Ek key se Claude, GPT, Gemini sab chalte hain, to provider badalna ho to sirf model ka naam badlega. Vercel kuch free credit deta hai, dashboard mein check kar lena.
   - Doosra option: tumhare portfolio assistant mein already **Gemini key** hai. Wahi use karna ho to `pnpm add @ai-sdk/google`, `.env` mein `GOOGLE_GENERATIVE_AI_API_KEY=...`, aur code mein `import { google } from '@ai-sdk/google'` karke `model: google('<jo Gemini model tum assistant mein use karte ho>')`. Baaki code same rahega.
4. **Key kabhi GitHub par push mat karna.** `.env` ko `.gitignore` mein daalo. (Interview mein bhi poochte hain: "API key frontend mein kyun nahi rakhte?" Jawab: browser mein jo bhi hai wo sab public hai.)

```bash
mkdir jobmatch-day1 && cd jobmatch-day1
pnpm init
pnpm add ai zod dotenv
pnpm add -D @types/node tsx typescript
echo "AI_GATEWAY_API_KEY=yahan_apni_key" > .env
echo ".env" >> .gitignore
```

---

## Part C: Code (step by step)

### Step 1: Sabse simple call (`hello.ts`)

```ts
import 'dotenv/config';
import { generateText } from 'ai';

const result = await generateText({
  model: 'anthropic/claude-sonnet-5.5', // AI Gateway ka model naam, koi bhi chalega
  instructions: 'You are a career coach for frontend developers. Answer in 3 short lines.',
  prompt: 'What should a React developer learn to work on AI products?',
  temperature: 0.3,
});

console.log(result.text);
console.log('Tokens used:', result.usage);
```

Chalao: `pnpm tsx hello.ts`

Dekho: jawab poora ek saath aaya. Aur `usage` mein input/output tokens dikhenge. Yahi bill hai.

### Step 2: Streaming (`stream.ts`)

```ts
import 'dotenv/config';
import { streamText } from 'ai';

const result = streamText({
  model: 'anthropic/claude-sonnet-5.5',
  prompt: 'Explain React useEffect to a beginner in 5 lines.',
});

for await (const piece of result.textStream) {
  process.stdout.write(piece); // har tukda aate hi print
}
console.log();
```

Farak dekho: text ek-ek karke aata hai. Kal yahi cheez Next.js UI mein karenge.

### Step 3: Memory waala chatbot (`chat.ts`)

```ts
import 'dotenv/config';
import { streamText, type ModelMessage } from 'ai';
import * as readline from 'node:readline/promises';

const terminal = readline.createInterface({ input: process.stdin, output: process.stdout });
const messages: ModelMessage[] = []; // yahi "memory" hai

while (true) {
  const userInput = await terminal.question('You: ');
  messages.push({ role: 'user', content: userInput });

  const result = streamText({
    model: 'anthropic/claude-sonnet-5.5',
    instructions: 'You help Ayush prepare for frontend + AI job interviews. Keep answers short.',
    messages, // poori history har baar jaa rahi hai
  });

  let full = '';
  process.stdout.write('\nAI: ');
  for await (const piece of result.textStream) {
    full += piece;
    process.stdout.write(piece);
  }
  process.stdout.write('\n\n');
  messages.push({ role: 'assistant', content: full }); // jawab bhi history mein
}
```

Chalao: `pnpm tsx chat.ts`. Pehle bolo "Mera naam Ayush hai", phir poocho "Mera naam kya hai?".

---

## Part D: Khud karo (asli learning yahan hai)

1. **Memory todo:** `chat.ts` mein `messages.push({ role: 'assistant', ... })` waali line comment karo. Ab kya hota hai? Kyun? (Ek line mein likho.)
2. **Temperature test:** `hello.ts` ko `temperature: 0` aur `temperature: 1` ke saath 3-3 baar chalao. Jawab kitne badalte hain?
3. **Token counter:** `chat.ts` mein har jawab ke baad `await result.usage` print karo. 5 message ke baad input tokens kitne badh gaye? Kyun? (Hint: Part A ka point 3.)
4. **Mini feature:** user `/reset` likhe to `messages` khaali ho jaye.
5. GitHub par `jobmatch-day1` naam se repo banao (ya `find-jobs/learning/` mein code daalo) aur push karo. `.env` push nahi hona chahiye.

---

## Part E: Interview sawal (bina dekhe jawab do)

1. Token kya hai, aur AI app ka cost kis par depend karta hai?
2. LLM ko pichli chat kaise "yaad" rehti hai?
3. Streaming se model fast hota hai kya? Phir fayda kya hai?
4. Temperature 0 kab rakhoge, 1 kab?
5. API key browser mein kyun nahi rakhte? Phir frontend se AI kaise call karte ho? (Hint: server route. Kal ka topic.)

Jawab mujhe thread mein bhejo, main check karunga.

---

**Kal (Day 2):** Yahi chatbot Next.js mein, `useChat` hook ke saath, proper streaming UI. JobMatch AI ka pehla screen.
