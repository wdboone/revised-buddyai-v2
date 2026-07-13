# Buddy AI — AI-Powered Life Coach

A single-file, zero-dependency web app that delivers personalized life coaching through a conversational interface powered by the Anthropic API. Built as a functional prototype demonstrating real-time AI coaching across eight life domains, with web-grounded responses, persistent user modeling, automatic topic classification, and account-based cross-device sync.

## Live Demo

Deploy by dropping `buddy-ai-v2.html` on any static host (GitHub Pages, Netlify, Vercel). No build step required.

## Features

| Feature | Status | Notes |
| --- | --- | --- |
| **Markdown rendering** | ✅ Live | marked + DOMPurify via CDN |
| **Chat history** | ✅ Live | Supabase Postgres — synced to your account |
| **Topic routing** | ✅ Live | Auto-classification via Claude Haiku |
| **Role alignment & guardrails** | ✅ Live | System prompt + regex pre-check |
| **User modeling** | ✅ Live | Persistent fact extraction with view/edit UI |
| **Web-grounded responses** | ✅ Live | Anthropic web_search tool, up to 3 searches/reply |
| **User accounts (email/password)** | ✅ Live | Supabase Auth |
| **Cross-device conversation sync** | ✅ Live | Supabase Postgres with Row-Level Security |
| **Server-side API proxy** | ⏳ Planned | Supabase Edge Function — keeps the Anthropic key off the browser |
| **Per-user rate limiting** | ⏳ Planned | Enforced at the Edge Function level |

## Architecture

```
buddy-ai-v2.html
│
├── UI Layer          Vanilla JS + CSS custom properties (no framework)
├── Markdown          marked@12 + DOMPurify@3 (CDN, no npm)
├── Auth              Supabase Auth — email/password, session persistence
├── Persistence       Supabase Postgres (profile, history) + localStorage (API key only)
├── Topic Router      Claude Haiku — lightweight classification call
├── Coaching Engine   Claude Sonnet 4.6 — with web_search tool (max 3/reply)
└── User Model        MEMO block parsed from assistant replies → stored facts
```

**Key architectural decisions:**

- **No build step.** The entire app is a single `.html` file with CDN-loaded dependencies. This makes GitHub Pages deployment trivial and keeps the prototype shareable as a raw file.
- **Two-model strategy.** Topic classification uses `claude-haiku-4-5-20251001` (fast, ~25× cheaper per token than Sonnet) while coaching uses `claude-sonnet-4-6`. This keeps latency and cost reasonable for a prototype.
- **Structured memory extraction.** Each assistant reply includes a hidden `<<<MEMO>>>` JSON block that the client parses to extract durable facts and category notes. This avoids a separate summarization call and keeps the user model updated incrementally.
- **Account-based persistence with Row-Level Security.** Profile and conversation data are stored in Supabase Postgres, scoped per user via RLS policies — a signed-in user's data is only ever reachable by that user, enforced at the database layer, not just in application code.
- **Direct browser → Anthropic API.** The `anthropic-dangerous-direct-browser-access` header enables this for prototyping. A future update will move this behind a Supabase Edge Function so the key never touches the browser.

## Setup

### 1. Get an Anthropic API key

Create one at [console.anthropic.com/settings/keys](https://console.anthropic.com/settings/keys). Standard API usage rates apply.

### 2. Set up Supabase

Create a project at [supabase.com](https://supabase.com), then run the schema + Row-Level Security setup SQL (see `BUDDY_AI_V2_UPGRADE_GUIDE.md`) in the SQL Editor. Copy your Project URL and anon/publishable key into the `SUPABASE_URL` and `SUPABASE_ANON_KEY` constants near the top of the `<script>` block in `buddy-ai-v2.html`.

### 3. Deploy

**GitHub Pages (recommended for demo):**

```
1. Push buddy-ai-v2.html to your repo
2. Settings → Pages → Deploy from branch → select main / root
3. Visit https://<your-username>.github.io/<repo-name>/buddy-ai-v2.html
```

**Local:**

```bash
# Any static server works — Python's built-in is the simplest
python3 -m http.server 8080
# Open http://localhost:8080/buddy-ai-v2.html
```

### 4. Connect your key

On first load, click the ⚙ icon and paste your `sk-ant-...` key. It is stored only in your browser's localStorage and sent directly to Anthropic — it never touches Supabase or any intermediate server.

## Life Coaching Domains

| Category | Focus |
| --- | --- |
| 💬 Just Talk | Open-ended — Buddy follows wherever the conversation goes |
| ❤️ Relationships | Partners, family, friendships, conflict, boundaries |
| 💼 Career & Direction | Job search, transitions, burnout, purpose in work |
| 💰 Finances | Budgeting mindset, debt, financial goal-setting (frameworks only — not financial advice) |
| 👨‍👩‍👧 Parenting & Family | Raising children, co-parenting, family dynamics |
| 🙏 Faith & Spiritual Guidance | Meaning, values, doubt, spiritual practice |
| 🤝 Workplace Ethics | Ethical dilemmas, conflict with coworkers/managers, integrity |
| 🌱 Personal Growth | Character, habits, self-discipline — anchored to the Beatitudes (Matt 5:3-10) as a character framework |

## Role Boundaries & Safety

Buddy operates under explicit system-prompt guardrails:

- **No credential claims** — will not represent itself as a licensed therapist, physician, attorney, or financial advisor
- **Out-of-scope deflection** — declines requests outside a coaching context with a warm redirect
- **Crisis protocol** — detects distress signals via regex pre-check (fires before the API call) and includes 988 / Crisis Text Line resources immediately; the system prompt reinforces this at the model level
- **AI disclosure** — answers honestly if directly asked whether it is a real person

## Data & Privacy

| Data | Where it lives | Shared? |
| --- | --- | --- |
| Your name / email | Supabase (tied to your account) | No — visible only to you, enforced by Row-Level Security |
| Conversation history | Supabase Postgres | No — protected by the same Row-Level Security policies |
| Extracted user facts | Supabase Postgres | No — protected by the same Row-Level Security policies |
| API key | localStorage (this browser only) | No — sent only to api.anthropic.com |

Conversation history and extracted facts now sync across devices via your account — log in from any device to pick up where you left off. Clearing browser storage no longer erases your data; it only clears your locally-stored Anthropic API key, which you'll need to re-enter. The Anthropic API key itself remains browser-local and is never sent to or stored in Supabase.

## Roadmap — Remaining Work

The following features still require additional backend work:

- [ ] **Server-side API proxy** — move the Anthropic key behind a Supabase Edge Function so the browser never holds it directly
- [ ] **Per-user rate limiting** — enforced at the Edge Function level

See [BUDDY_AI_V2_UPGRADE_GUIDE.md](https://github.com/wdboone/revised-buddyai-v2/blob/main/BUDDY_AI_V2_UPGRADE_GUIDE.md) for the full step-by-step implementation plan.

## Tech Stack

| Layer | Technology |
| --- | --- |
| UI | Vanilla HTML/CSS/JS — no framework |
| Markdown | [marked](https://github.com/markedjs/marked) + DOMPurify |
| Auth & Database | Supabase (Auth + Postgres with Row-Level Security) |
| AI (coaching) | claude-sonnet-4-6 with web_search_20250305 tool |
| AI (routing) | claude-haiku-4-5-20251001 |
| Persistence | Supabase Postgres (profile, history) + browser localStorage (API key) |
| Hosting | GitHub Pages / any static host |

## License
