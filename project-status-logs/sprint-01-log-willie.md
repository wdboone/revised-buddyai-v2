# MSAI 5573 · AI Studio II — Individual Sprint Log (Willie Boone)

## 1. Sprint information

| | |
|---|---|
| **Project / Team** | Buddy AI — AI-powered life coach |
| **Sprint number** | Sprint 1 |
| **Week of (start – end)** | 06/30/2026 – 07/06/2026 |
| **Team sprint goal** | Deliver an initial prototype/mockup for the AI coaching application. |
| **My focus this sprint** | Design the architecture and ship a working concept demo. |

## 2. My standup answers

| | |
|---|---|
| **Done since last standup** | Designed the overall app architecture: single HTML file, Claude API integration, sidebar navigation with 5 life-domain tabs, API-key connect flow. Built a working chat interface calling the Claude API directly, with 5 per-domain system prompts (Relationships, Finances, Spirituality, Career, Family). Implemented client-side crisis language detection (regex-based), a persistent non-dismissible disclaimer, and an API-key browser-memory-only flow. Documented known limitations and next steps (client-side key handling, no cross-session memory, regex crisis detection, no auth or persistence). |
| **Plan before next standup** | Continue prototype development toward a working v2. |
| **Blockers / help needed** | None. |

## 3. Board snapshot

See the team sprint log (`sprint-01-log.md`) for the shared board snapshot — no columns were populated yet this early in the project.

## 4. Blockers & risks I owned

| Blocker / risk | Impact | Status |
|---|---|---|
| API key is client-side only, browser-memory-only | Not production-safe; acceptable for a v1 demo | Documented as a known limitation; addressed in Sprint 4 |
| No session persistence | Tab switching resets conversation context | Documented as a known limitation; addressed in Sprint 3 |

## 5. Decisions I made or contributed to

| Decision | Why | Date |
|---|---|---|
| Team role assignments — I lead prototype/application development; Hunter leads the research informing the build, plus architecture guidance & testing. | Play to each member's strengths and keep the research and the build aligned. | 06/30 |
| Ship as a single HTML file with no build step. | Fastest path to a working, testable demo. | 07/01 |

## 6. Action items & next steps

| Action / next step | Due | Link |
|---|---|---|
| Identify known limitations; plan v2 architecture (backend proxy, cross-domain memory, improved crisis detection). | Sprint 2 | github.com/wdboone/revised-buddyai-v2 |

## 7. My sprint reflection

**What went well:** Went from zero to a working, demoable product in one sprint — the concept demo, five coaching personas, and a first-pass safety layer all shipped together.

**What slowed me down:** Nothing significant. This sprint was scoped conservatively on purpose, to get something real in front of the team fast.

**What I'll change next sprint:** Move faster on backend and session-persistence concerns now that the core concept is proven and I know the real gaps.

## 8. Links & artifacts

| | |
|---|---|
| **GitHub repository** | https://github.com/wdboone/revised-buddyai-v2 |
| **Deliverable(s) this sprint** | concept-demo.html (v1) — working chat UI; crisis detection module; disclaimer UI; known-limitations documentation |
