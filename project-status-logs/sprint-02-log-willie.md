# MSAI 5573 · AI Studio II — Individual Sprint Log (Willie Boone)

## 1. Sprint information

| | |
|---|---|
| **Project / Team** | Buddy AI — AI-powered life coach |
| **Sprint number** | Sprint 2 |
| **Week of (start – end)** | 07/07/2026 – 07/13/2026 |
| **Team sprint goal** | Turn the mockup into a working demo with the core coaching features. |
| **My focus this sprint** | Rebuild the demo into a feature-complete v2. |

## 2. My standup answers

| | |
|---|---|
| **Done since last standup** | Added Markdown rendering to assistant replies (marked + DOMPurify via CDN), styled inside chat bubbles. Built localStorage-based chat history: create, persist, resume, and delete conversations, with a sidebar history panel. Implemented automatic topic routing using Claude Haiku to classify the user's first message into one of 8 life domains, with a silent category switch and toast notification. Added role-alignment guardrails to the system prompt, plus a client-side regex crisis pre-check with immediate display of 988 resources. Built persistent user modeling: MEMO-block extraction from assistant replies stores durable facts, with a "What Buddy knows" panel to view/edit/add. Enabled the Anthropic web_search tool (max 3/reply) for web-grounded responses, with citation sources surfaced below each reply. Published the app to GitHub and wrote the full README (architecture, setup, feature table, data/privacy, roadmap). |
| **Plan before next standup** | Harden the demo and start on user accounts and cross-device sync. |
| **Blockers / help needed** | None. |

## 3. Board snapshot

See the team sprint log (`sprint-02-log.md`) for the shared board snapshot as of 07/13.

## 4. Blockers & risks I owned

| Blocker / risk | Impact | Status |
|---|---|---|
| The demo calls the AI service and holds its key directly in the browser | Fine for a demo, not safe for real users | Open — planned for a later sprint |
| Chat history and user modeling store data on the device only | Will need refactoring once a database and accounts are introduced | Open — revisit when server/database lands |

## 5. Decisions I made or contributed to

| Decision | Why | Date |
|---|---|---|
| Use a two-model design — Claude Haiku to route the topic, Claude Sonnet to coach. | Keeps replies good while holding down latency and cost. | 07/07 |
| Extract user facts from each reply and store them on the device. | Gives the app a working user model to build coaching on, and matches Hunter's research direction. | 07/07 (team decision) |

## 6. Action items & next steps

| Action / next step | Due | Link |
|---|---|---|
| Harden the demo; begin user accounts and cross-device sync. | Sprint 3 | github.com/wdboone/revised-buddyai-v2 |

## 7. My sprint reflection

**What went well:** Six major features shipped in one sprint — Markdown rendering, chat history, topic routing, guardrails, user modeling, and web search — without a build system slowing anything down.

**What slowed me down:** Nothing blocking. The scope was ambitious but manageable inside a single-file architecture.

**What I'll change next sprint:** Prioritize real accounts next, since every feature I shipped this sprint currently resets per device.

## 8. Links & artifacts

| | |
|---|---|
| **GitHub repository** | https://github.com/wdboone/revised-buddyai-v2 |
| **Deliverable(s) this sprint** | Markdown rendering module; chat history system; topic routing module (inferCategory); guardrails system prompt blocks + crisis pre-check; user model module + profile panel UI; web search integration; README.md |
