# Buddy AI — AI-Powered Life Coach

A single-file, zero-dependency web app that delivers personalized life coaching through a conversational interface powered by the Anthropic API. Built as a functional prototype demonstrating real-time AI coaching across eight life domains, with web-grounded responses, persistent user modeling, and automatic topic classification.

---

## Live Demo

> Deploy by dropping `buddy-ai-v2.html` on any static host (GitHub Pages, Netlify, Vercel). No build step required.

---

## Features

| Feature | Status | Notes |
|---|---|---|
| **Markdown rendering** | ✅ Live | `marked` + `DOMPurify` via CDN |
| **Chat history** | ✅ Live | `localStorage` — device-scoped |
| **Topic routing** | ✅ Live | Auto-classification via Claude Haiku |
| **Role alignment & guardrails** | ✅ Live | System prompt + regex pre-check |
| **User modeling** | ✅ Live | Persistent fact extraction with view/edit UI |
| **Web-grounded responses** | ✅ Live | Anthropic `web_search` tool, up to 3 searches/reply |
| **User accounts (email/password)** | ⏳ v3 | Requires Supabase Auth |
| **Cross-device conversation sync** | ⏳ v3 | Requires Supabase Postgres + RLS |

---

## Architecture

```
buddy-ai-v2.html
│
├── UI Layer          Vanilla JS + CSS custom properties (no framework)
├── Markdown          marked@12 + DOMPurify@3 (CDN, no npm)
├── Persistence       localStorage (profile, history, API key)
├── Topic Router      Claude Haiku — lightweight classification call
├── Coaching Engine   Claude Sonnet 4.6 — with web_search tool (max 3/reply)
└── User Model        MEMO block parsed from assistant replies → stored facts
```

**Key architectural decisions:**

- **No build step.** The entire app is a single `.html` file with CDN-loaded dependencies. This makes GitHub Pages deployment trivial and keeps the prototype shareable as a raw file.
- **Two-model strategy.** Topic classification uses `claude-haiku-4-5-20251001` (fast, ~25× cheaper per token than Sonnet) while coaching uses `claude-sonnet-4-6`. This keeps latency and cost reasonable for a prototype.
- **Structured memory extraction.** Each assistant reply includes a hidden `<<<MEMO>>>` JSON block that the client parses to extract durable facts and category notes. This avoids a separate summarization call and keeps the user model updated incrementally.
- **Direct browser → Anthropic API.** The `anthropic-dangerous-direct-browser-access` header enables this for prototyping. The v3 roadmap moves this behind a Supabase Edge Function so the key never touches the browser.

---

## Setup

### 1. Get an Anthropic API key

Create one at [console.anthropic.com/settings/keys](https://console.anthropic.com/settings/keys). Standard API usage rates apply.

### 2. Deploy

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

### 3. Connect your key

On first load, click the ⚙ icon and paste your `sk-ant-...` key. It is stored only in your browser's `localStorage` and sent directly to Anthropic — it never touches any intermediate server.

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
| 🤝 Workplace Ethics | Ethical dilemmas, conflict with coworkers/managers, integrity |
| 🌱 Personal Growth | Character, habits, self-discipline — anchored to the Beatitudes (Matt 5:3-10) as a character framework |

---

## Role Boundaries & Safety

Buddy operates under explicit system-prompt guardrails:

- **No credential claims** — will not represent itself as a licensed therapist, physician, attorney, or financial advisor
- **Out-of-scope deflection** — declines requests outside a coaching context with a warm redirect
- **Crisis protocol** — detects distress signals via regex pre-check (fires before the API call) and includes 988 / Crisis Text Line resources immediately; the system prompt reinforces this at the model level
- **AI disclosure** — answers honestly if directly asked whether it is a real person

---

## Data & Privacy

| Data | Where it lives | Shared? |
|---|---|---|
| Your name | `localStorage` (this browser only) | No |
| Conversation history | `localStorage` (this browser only) | No |
| Extracted user facts | `localStorage` (this browser only) | No |
| API key | `localStorage` (this browser only) | No — sent only to `api.anthropic.com` |

Nothing is stored on any server in the current version. Clearing browser storage erases all local data.

---

## Roadmap — v3 (Supabase)

The following features require a backend and are scoped for the next version:

- [ ] **User accounts** — email/password signup and login via Supabase Auth
- [ ] **Cross-device sync** — conversations and user model stored in Supabase Postgres with Row-Level Security
- [ ] **Server-side API proxy** — Supabase Edge Function holds the Anthropic key; browser never sees it
- [ ] **Per-user rate limiting** — enforced at the Edge Function level

See [`BUDDY_AI_V2_UPGRADE_GUIDE.md`](./BUDDY_AI_V2_UPGRADE_GUIDE.md) for the full step-by-step implementation plan.

---

## Tech Stack

| Layer | Technology |
|---|---|
| UI | Vanilla HTML/CSS/JS — no framework |
| Markdown | [marked](https://github.com/markedjs/marked) + [DOMPurify](https://github.com/cure53/DOMPurify) |
| AI (coaching) | `claude-sonnet-4-6` with `web_search_20250305` tool |
| AI (routing) | `claude-haiku-4-5-20251001` |
| Persistence | Browser `localStorage` |
| Hosting | GitHub Pages / any static host |

---

## License

MIT — free to use, modify, and build on.

---

*Built as a prototype. Not a substitute for licensed mental health, medical, legal, or financial services.*
