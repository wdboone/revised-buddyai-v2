# MSAI — Activity & Deliverables Log

**Student:** Willie Boone
**Cohort:** Summer
**Course:** Studio II
**Project/Client:** AI Life Coach
**Team members:** Willie Boone, Hunter Phillips
**Professor:** Gilberto Díaz Casañas

---

## Weekly Standup Notes

| Week / Date | Done since last standup | Planned before next standup | Blockers, risks & decisions |
| --- | --- | --- | --- |
| Week 1 · 07/01 | Built Buddy AI v1 concept demo (single HTML file): working chat interface with Claude API integration, 5 life-domain system prompts, sidebar navigation, API key connect flow, crisis language detection, and persistent disclaimer. | Identify known limitations; plan v2 architecture with backend API proxy, cross-domain memory, and improved crisis detection. | API key is client-side only — not production-safe; no session persistence; tab switching resets conversation context. |
| Week 2 · 07/08 | Built Buddy AI v2: added Markdown rendering, localStorage chat history, auto topic routing (Claude Haiku), role alignment guardrails, user modeling with view/edit UI, and web-grounded responses via Anthropic web_search tool. | Implement Supabase backend for user accounts, cross-device sync, and server-side API key proxy (v3 roadmap). | No blockers. Supabase integration deferred to v3; device-only storage is an accepted limitation for the prototype. |

---

## Activity Log

| Date | Wk | Activity — what you did | Deliverable(s) it created or advanced | Role | Status/hrs | URL |
| --- | --- | --- | --- | --- | --- | --- |
| 07/01 | 1 | Designed overall app architecture: single HTML file, Claude API integration, sidebar navigation with 5 life-domain tabs, API key connect flow. | App architecture plan; system prompt framework | Created | Complete · 2h | github.com/wdboone/revised-buddyai-v2 |
| 07/01 | 1 | Built a working chat interface calling the Claude API directly; implemented 5 per-domain system prompts (Relationships, Finances, Spirituality, Career, Family). | concept-demo.html (v1) — working chat UI | Created | Complete · 4h | github.com/wdboone/revised-buddyai-v2 |
| 07/01 | 1 | Implemented client-side crisis language detection (regex-based); added persistent non-dismissible disclaimer; added API key browser-memory-only flow. | Crisis detection module; disclaimer UI; API key connect flow | Created | Complete · 2h | github.com/wdboone/revised-buddyai-v2 |
| 07/01 | 1 | Documented known limitations and next steps: client-side key handling, no cross-session memory, regex crisis detection, no auth or persistence. | Known limitations + next steps documentation (README section) | Created | Complete · 1h | github.com/wdboone/revised-buddyai-v2 |
| 07/08 | 2 | Added Markdown rendering to assistant replies using marked + DOMPurify via CDN; styled formatted output (bold, lists, headers, blockquotes) inside chat bubbles. | Markdown rendering module integrated into buddy-ai-v2.html | Created | Complete · 1.5h | github.com/wdboone/revised-buddyai-v2 |
| 07/08 | 2 | Built localStorage-based chat history: create, persist, resume, and delete conversations; sidebar history panel with relative dates and delete buttons. | Chat history system; history UI in sidebar | Created | Complete · 3h | github.com/wdboone/revised-buddyai-v2 |
| 07/08 | 2 | Implemented automatic topic routing using Claude Haiku to classify the user's first message into one of 8 life domains; silent category switch with toast notification. | Topic routing module (inferCategory function) | Created | Complete · 1.5h | github.com/wdboone/revised-buddyai-v2 |
| 07/08 | 2 | Added role-alignment guardrails to the system prompt (role boundaries, credential claims, crisis protocol); added client-side regex crisis pre-check with immediate 988 resource display. | Guardrails system prompt blocks; crisis pre-check (detectCrisis) | Created | Complete · 1.5h | github.com/wdboone/revised-buddyai-v2 |
| 07/08 | 2 | Built persistent user modeling: MEMO block extraction from assistant replies stores durable facts in localStorage; "What Buddy knows" slide-in panel with edit/delete/add. | User model module; profile panel UI | Created | Complete · 2h | github.com/wdboone/revised-buddyai-v2 |
| 07/08 | 2 | Enabled Anthropic web_search tool (max 3/reply) for web-grounded responses; surfaced citation sources below each reply; updated typing indicator to "checking the web…" | Web search integration; source citation UI | Created | Complete · 1h | github.com/wdboone/revised-buddyai-v2 |
| 07/08 | 2 | Published app to GitHub (revised-buddyai-v2 repo); wrote full README with architecture, setup instructions, feature table, data/privacy table, and roadmap; added repo description and topics. | README.md; GitHub repo (revised-buddyai-v2) | Created | Complete · 1.5h | github.com/wdboone/revised-buddyai-v2 |

---

## Deliverables Register

| Deliverable | Type | Role | Specific contribution | Status | Link |
| --- | --- | --- | --- | --- | --- |
| Buddy AI v1 Concept Demo (concept-demo.html) | Code / App | Created | Built entire single-file prototype: chat UI, 5 domain system prompts, API connect flow, crisis detection, persistent disclaimer. | Complete | github.com/wdboone/revised-buddyai-v2 |
| Per-domain system prompt framework (v1) | Design / Docs | Created | Designed and wrote 5 domain-specific system prompts with guardrails forbidding credential claims. | Complete | github.com/wdboone/revised-buddyai-v2 |
| Crisis detection module (regex pre-check) | Code | Created | Wrote client-side regex patterns detecting self-harm language; surfaces 988/Crisis Text Line resources before the API response arrives. | Complete | github.com/wdboone/revised-buddyai-v2 |
| Buddy AI v2 (buddy-ai-v2.html) | Code / App | Created | Full v2 rebuild: Markdown rendering, localStorage chat history, topic routing, guardrails, user modeling, web-grounded responses via web_search tool. | Complete | github.com/wdboone/revised-buddyai-v2 |
| Chat history system (localStorage) | Code | Created | Built a create/persist/resume/delete conversation flow with a sidebar history panel showing relative dates. | Complete | github.com/wdboone/revised-buddyai-v2 |
| Auto topic routing module (Claude Haiku) | Code | Created | The inferCategory() function calls Haiku to classify the user's first message into 8 life domains; a silent switch with a toast notification. | Complete | github.com/wdboone/revised-buddyai-v2 |
| User modeling + profile panel UI | Code | Created | MEMO block extraction stores durable user facts in localStorage; the slide-in panel lets the user view, edit, delete, and manually add facts. | Complete | github.com/wdboone/revised-buddyai-v2 |
| README.md + GitHub repo documentation | Documentation | Created | Wrote full README: feature table, architecture diagram, setup instructions, data/privacy table, tech stack, and v3 Supabase roadmap. | Complete | github.com/wdboone/revised-buddyai-v2 |

---

## Mid-Term Summary

### 1. Project overview

AI Life Coach (Buddy AI) is a conversational web app that delivers personalized life coaching across eight domains, powered by the Anthropic API. My role has been primary developer on the client-side application — architecture, feature implementation, and documentation.

### 2. Activities completed this period

**Week 1:** Designed and built the initial concept demo — a single-file HTML app with a working Claude API chat interface, five life-domain system prompts, sidebar navigation, an API key connect flow, and client-side crisis language detection.

**Week 2:** Rebuilt the app as v2 — added Markdown rendering, localStorage-backed chat history (create/resume/delete conversations), automatic topic routing via Claude Haiku, role-alignment guardrails in the system prompt, persistent user modeling with a view/edit UI, and web-grounded responses via the Anthropic web_search tool.

### 3. Deliverables created or contributed to

- **Concept Demo (v1)** — Created. Full working prototype with chat, five domain prompts, crisis detection, and disclaimer.
- **Buddy AI v2** — Created. Full rebuild adding Markdown rendering, chat history, topic routing, guardrails, user modeling, and web search.
- **Crisis detection module** — Created. Regex-based pre-check surfacing 988/Crisis Text Line resources before any API call.
- **User modeling + profile panel** — Created. MEMO-block fact extraction with a view/edit/delete UI.
- **README.md** — Created. Full architecture, setup, feature, and privacy documentation.

Status: all listed deliverables are Complete as of Week 2.

### 4. Collaboration & contribution

*(Fill in: how you and Hunter divided or coordinated work, what was reviewed jointly, and anything you built on top of teammate contributions.)*

### 5. Challenges, blockers & decisions

Key early decision: the API key is stored and used client-side only for this prototype phase — a known limitation, not production-safe, and intentionally deferred rather than solved in v1/v2. No blocking issues in Weeks 1–2; Supabase backend integration (accounts, cross-device sync, server-side key proxy) was consciously scoped out to v3 rather than attempted early.

### 6. Plan for the second half

Implement the Supabase backend: user accounts (email/password), Row-Level Security-scoped data storage, and cross-device conversation sync — already underway as of this log. Remaining after that: move the Anthropic API key behind a server-side proxy (Supabase Edge Function) and add per-user rate limiting.

### 7. Self-assessment (strengths and struggles)

*(Write this yourself — an honest reflection on your own progress and where you're struggling. This section should be in your own voice, not drafted for you.)*
