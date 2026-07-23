# Buddy AI — AI-Powered Life Coach

A web app that delivers personalized life coaching through a conversational interface powered by the Anthropic API. Built as a functional prototype with real user accounts, cloud-synced conversation history, web-grounded responses, and a user model that learns from both conversation and uploaded documents.

---

## Live App

**[https://wdboone.github.io/revised-buddyai-v2/](https://wdboone.github.io/revised-buddyai-v2/)**

Sign up with an email and password. Your conversations and profile sync across any device you log in from.

---

## Features

| Feature | Status | Notes |
|---|---|---|
| **Markdown rendering** | ✅ Live | `marked` + `DOMPurify` via CDN |
| **User accounts** | ✅ Live | Email/password via Supabase Auth |
| **Chat history** | ✅ Live | Persisted in Supabase Postgres, synced across devices |
| **Topic routing** | ✅ Live | Auto-classification via Claude Haiku |
| **Role alignment & guardrails** | ✅ Live | System prompt + client-side crisis pre-check |
| **User modeling** | ✅ Live | Fact extraction from conversation + view/edit profile panel |
| **File upload → fact extraction** | ✅ Live | `.txt` and `.md` files; AI extracts personal facts on upload |
| **Web-grounded responses** | ✅ Live | Anthropic `web_search` tool, up to 3 searches per reply |
| **Server-side API key** | ✅ Live | Anthropic key stored in Supabase Edge Function secret — never in the browser |
| **PDF file upload** | ⏳ Planned | Requires `pdf.js` — deferred to next release |

---

## Architecture

```
index.html  (single-file frontend)
│
├── UI Layer          Vanilla JS + CSS custom properties
├── Markdown          marked@12 + DOMPurify@3 (CDN)
├── Auth              Supabase Auth (email/password, session persistence)
├── Database          Supabase Postgres (profiles + conversations, RLS enforced)
├── Topic Router      Claude Haiku — lightweight first-message classification
├── Edge Function     Supabase Edge Function — holds the Anthropic API key server-side
└── Coaching Engine   Claude Sonnet 4.6 — with web_search tool (max 3/reply)
```

**Key architectural decisions:**

- **No build step.** The entire frontend is a single `index.html` with CDN-loaded dependencies. Deployable to any static host instantly.
- **Server-side API key.** The Anthropic API key lives in a Supabase Edge Function secret. The browser never sees or transmits it. All AI calls route through the Edge Function, which verifies the user's session before forwarding the request.
- **Two-model strategy.** Topic classification uses `claude-haiku-4-5-20251001` (fast, low cost) while coaching uses `claude-sonnet-4-6` (full capability). This keeps latency and cost reasonable.
- **Incremental user modeling.** Each assistant reply includes a hidden `<<<MEMO>>>` JSON block that the client parses to extract durable facts. Facts are stored in Supabase and injected back into the system prompt on future conversations — without a separate summarization call.
- **Row-Level Security.** Every Supabase table has RLS policies ensuring users can only ever read and write their own data. This applies automatically to conversation history, profile facts, and any facts extracted from uploaded files.

---

## Setup — For Users

**1.** Open the live app: [https://wdboone.github.io/revised-buddyai-v2/](https://wdboone.github.io/revised-buddyai-v2/)

**2.** Click **Get started** → **Create your account** → enter your email and password.

**3.** Check your email for a confirmation link and click it. You will be brought back to the app and logged in automatically.

**4.** Start talking to Buddy. That's it — no API keys, no setup, no configuration.

---

## Setup — For Developers (deploying your own instance)

**1. Supabase project**

- Create a project at [supabase.com](https://supabase.com)
- Run the SQL schema below in the SQL Editor
- Under Authentication → URL Configuration, set **Site URL** to your deployment URL
- Under Authentication → Providers → Email, configure email confirmation settings as needed

**2. Database schema**

```sql
create table profiles (
  user_id        uuid primary key references auth.users(id) on delete cascade,
  first_met      timestamptz,
  last_seen      timestamptz,
  session_count  int default 0,
  memory_facts   jsonb default '[]',
  category_notes jsonb default '{}'
);

create table conversations (
  id         uuid primary key default gen_random_uuid(),
  user_id    uuid references auth.users(id) on delete cascade not null,
  title      text not null default 'New conversation',
  category   text not null default 'general',
  messages   jsonb default '[]',
  updated_at timestamptz default now()
);

alter table profiles      enable row level security;
alter table conversations enable row level security;

create policy "own profile"       on profiles      for all using (auth.uid() = user_id);
create policy "own conversations" on conversations for all using (auth.uid() = user_id);
```

**3. Supabase Edge Function**

- Go to Edge Functions → Deploy a new function → name it `chat`
- Paste in the Edge Function code (see `/supabase/functions/chat/index.ts` or the Issue #11 reference guide)
- Under Edge Functions → Secrets, add: `ANTHROPIC_API_KEY` = your `sk-ant-...` key

**4. Frontend configuration**

In `index.html`, update these two lines near the top of the script block:

```js
const SUPABASE_URL  = "https://your-project-id.supabase.co";
const SUPABASE_ANON_KEY = "your-anon-key-here";
```

**5. Deploy**

Upload `index.html` to any static host — GitHub Pages, Vercel, or Netlify. No build step required.

---

## Life Coaching Domains

| Category | Focus |
|---|---|
| 💬 Just Talk | Open-ended — Buddy follows wherever the conversation goes |
| ❤️ Relationships | Partners, family, friendships, conflict, boundaries |
| 💼 Career & Direction | Job search, transitions, burnout, purpose in work |
| 💰 Finances | Budgeting mindset, debt, financial goal-setting (frameworks only — not financial advice) |
| 👨‍👩‍👧 Parenting & Family | Raising children, co-parenting, family dynamics |
| 🙏 Faith & Spiritual Guidance | Meaning, values, doubt, spiritual practice |
| 🤝 Workplace Ethics | Ethical dilemmas, conflict with coworkers or managers, integrity |
| 🌱 Personal Growth | Character, habits, self-discipline — anchored to the Beatitudes (Matt 5:3–10) as a character compass |

---

## Role Boundaries & Safety

Buddy operates under explicit system-prompt guardrails:

- **No credential claims** — will not represent itself as a licensed therapist, physician, attorney, or financial advisor
- **Out-of-scope deflection** — declines requests outside coaching with a warm redirect using a defined pattern: acknowledge → explain → redirect
- **Crisis protocol** — detects distress signals via regex pre-check (fires before the API call) and includes 988 / Crisis Text Line resources immediately; the system prompt reinforces this at the model level
- **AI disclosure** — answers honestly if directly asked whether it is a real person

---

## Data & Privacy

| Data | Where it lives | Shared? |
|---|---|---|
| Your email and account | Supabase Auth | No — private to your account |
| Conversation history | Supabase Postgres (RLS) | No — only accessible when logged in as you |
| Profile facts | Supabase Postgres (RLS) | No — only accessible when logged in as you |
| Anthropic API key | Supabase Edge Function secret | No — never touches the browser |

The Anthropic API key is stored as an encrypted server-side secret. It is never stored in the browser, never transmitted from the browser, and never visible to users.

---

## Tech Stack

| Layer | Technology |
|---|---|
| UI | Vanilla HTML/CSS/JS — no framework |
| Markdown | [marked](https://github.com/markedjs/marked) + [DOMPurify](https://github.com/cure53/DOMPurify) |
| Auth & Database | [Supabase](https://supabase.com) (Auth + Postgres + Edge Functions) |
| API proxy | Supabase Edge Function (Deno/TypeScript) |
| AI — coaching | `claude-sonnet-4-6` with `web_search_20250305` tool |
| AI — routing & file extraction | `claude-haiku-4-5-20251001` |
| Hosting | GitHub Pages |

---

## Project Context

Built as a capstone prototype for the Master of Science in Applied Artificial Intelligence program, Studio II — Summer 2026.

---

## License

MIT — free to use, modify, and build on.

---

*Buddy AI is an AI life coach companion — not a substitute for licensed mental health, medical, legal, or financial services. If you are in crisis, call or text 988.*
