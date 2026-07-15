# MSAI 5573 · AI Studio II — Team Weekly Sprint Log

## 1. Sprint information

| | |
|---|---|
| **Project / Team** | Buddy AI — AI-powered life coach |
| **Sprint number** | Sprint 3 |
| **Week of (start – end)** | 07/14/2026 – 07/20/2026 |
| **Sprint goal (one sentence)** | Ship user accounts with cross-device sync, and settle which user-model representation the build should use. |
| **Facilitator / scribe** | Hunter Phillips |
| **Members present** | Hunter Phillips, Willie Boone |
| **Members absent** | None |

## 2. Standup round-robin

| Team member | Done since last standup | Plan before next standup | Blockers / help needed |
|---|---|---|---|
| Willie Boone | Shipped email/password auth and migrated profile and conversation storage from browser localStorage to per-user Postgres tables with RLS (accounts + cross-device sync, #3); fixed user-model fact handling so Buddy references known facts (#7); grounded replies in the real device date. | Fix the email-confirmation redirect (#8); continue toward the server-side API-key proxy. | Email confirmation link redirects to a broken origin (#8). |
| Hunter Phillips | Finished the four versions on the personal dataset and ran the evaluation (raw came out on top); caught that the structured versions had been built lossily, so redesigned to a clean three-version lossless comparison and rebuilt it; re-ran the evaluation with a stronger judge setup and a human pass. Raw still wins, this time without the confound. | Report the recommendation to the team; if we firm it up, test on real user dilemmas with length-controlled replies. | None. |

## 3. Board snapshot (GitHub Project)

| Date | Backlog | Ready | In Progress | In Review | Done | Notes |
|---|---|---|---|---|---|---|
| 07/15 | Server-side API proxy; file upload (#10) | Email-confirmation fix (#8) | Guardrails spike (#9); evals | | Markdown rendering (#2); chat history (#4); topic routing (#5); user accounts + sync (#3); user modeling (#7); role alignment & guardrails (#6) | Issues: https://github.com/wdboone/revised-buddyai-v2/issues |

## 4. Blockers & risks

| Blocker / risk | Impact | Owner | Action to resolve | Status |
|---|---|---|---|---|
| Email confirmation link redirects to a broken origin (localhost:3000) (#8) | Blocks new users from finishing signup | Willie | Point the Supabase auth URL config at the app's real host (e.g. a GitHub Pages URL) | Open |
| Anthropic API key is still held in the browser | Fine for a demo, not safe for real users | Willie | Move the key and calls behind a server-side proxy (roadmap) | Open |

## 5. Decisions made

| Decision | Why | Owner | Date |
|---|---|---|---|
| Migrate storage from browser localStorage to per-user Supabase tables with RLS, and add email/password auth. | Enables real accounts and cross-device sync. | Willie | 07/12 |
| Rebuild the user-model comparison losslessly and drop the extracted-fact version. | The structured versions were built by rewriting the history, which lost detail and confounded the result; a lossless design isolates arrangement as the only variable. | Hunter | 07/13 |
| Recommend feeding the coach the raw history over a distilled fact panel while it fits in context; keep fact-extraction for retention and scale, not quality. | With information held constant, the raw version beat every structured one on coaching quality, most clearly in the human pass. | Hunter | 07/15 |

## 6. Action items & next steps

| Action / next step | Owner | Due | Link (PR / issue / story) |
|---|---|---|---|
| Fix the email-confirmation redirect. | Willie | Next standup | https://github.com/wdboone/revised-buddyai-v2/issues/8 |
| Continue toward the server-side API-key proxy. | Willie | Next standup | https://github.com/wdboone/revised-buddyai-v2/issues |
| Report the user-modeling recommendation to the team. | Hunter | Next standup | — |
| If firming up the finding: test on real user dilemmas with length-controlled replies. | Hunter | Next standup | — |

## 7. Sprint reflection

| Reflection prompt | Team's notes |
|---|---|
| **What went well this sprint?** | Shipped email/password auth and cross-device sync; reached a clear result on how to represent the user model, confirmed by the human pass. |
| **What slowed us down?** | The first evaluation was confounded: the structured versions had been built lossily, which forced a redesign and rebuild. |
| **What will we change next sprint?** | Length-control the coach replies and test on real user dilemmas to firm up the finding. |

## 8. Links & artifacts

| | |
|---|---|
| **GitHub repository** | https://github.com/wdboone/revised-buddyai-v2 |
| **GitHub Project board** | https://github.com/wdboone/revised-buddyai-v2/issues |
| **Discussions** | n/a |
| **Prompt docs / artifacts** | Example deliverables: `project-status-logs/deliverables/` |
