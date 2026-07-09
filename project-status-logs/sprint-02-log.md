# MSAI 5573 · AI Studio II — Team Weekly Sprint Log

## 1. Sprint information

| | |
|---|---|
| **Project / Team** | Buddy AI — AI-powered life coach |
| **Sprint number** | Sprint 2 |
| **Week of (start – end)** | 07/07/2026 – 07/13/2026 |
| **Sprint goal (one sentence)** | Turn the mockup into a working demo with the core coaching features. |
| **Facilitator / scribe** | Hunter Phillips |
| **Members present** | Hunter Phillips, Willie Boone |
| **Members absent** | None |

## 2. Standup round-robin

| Team member | Done since last standup | Plan before next standup | Blockers / help needed |
|---|---|---|---|
| Willie Boone | Built the new demo app with the core coaching features: markdown rendering, chat history, topic routing, and user fact extraction. | Harden the demo and start on user accounts and cross-device sync. | None. |
| Hunter Phillips | Finished the personal persona dataset; upgraded and ran the automated evaluation across the four user-model versions and recorded the first results; began building the four versions from the personal dataset; reviewed the new demo. | Finish the four versions on the personal dataset, run the evaluation, and fold the findings into the build's user-modeling approach. | None. |

## 3. Board snapshot (GitHub Project)

| Date | Backlog | Ready | In Progress | In Review | Done | Notes |
|---|---|---|---|---|---|---|
| 07/13 | Server / database; user accounts | | User modeling; evals | | | Issues tracked at https://github.com/wdboone/revised-buddyai-v2/issues |

## 4. Blockers & risks

| Blocker / risk | Impact | Owner | Action to resolve | Status |
|---|---|---|---|---|
| The demo calls the AI service and holds its key directly in the browser | Fine for a demo, not safe for real users | Willie | Move the key and the calls behind a server before any public use | Open (planned for a later sprint) |

## 5. Decisions made

| Decision | Why | Owner | Date |
|---|---|---|---|
| Use a two-model design in the demo — a fast model to route the topic, a stronger model to coach. | Keeps replies good while holding down latency and cost. | Willie | 07/07 |
| Extract user facts from each reply and store them on the device. | Gives the app a working user model to build coaching on, and matches the research direction. | Team | 07/07 |
| Drop simple recall questions from the evaluation; keep synthesis and advice. | Recall doesn't separate the user-model versions; synthesis and advice do. | Hunter | 07/08 |

## 6. Action items & next steps

| Action / next step | Owner | Due | Link (PR / issue / story) |
|---|---|---|---|
| Harden the demo; begin user accounts and cross-device sync. | Willie | Next standup | https://github.com/wdboone/revised-buddyai-v2/issues |
| Finish the four user-model versions on the personal dataset and run the evaluation. | Hunter | Next standup | — |
| Report which user-modeling approach to carry into the build. | Hunter | Next standup | — |

## 7. Sprint reflection

| Reflection prompt | Team's notes |
|---|---|
| **What went well this sprint?** | Shipped a working demo with the core coaching features; got the first evaluation results comparing the user-model versions. |
| **What slowed us down?** | n/a |
| **What will we change next sprint?** | n/a |

## 8. Links & artifacts

| | |
|---|---|
| **GitHub repository** | https://github.com/wdboone/revised-buddyai-v2 |
| **GitHub Project board** | https://github.com/wdboone/revised-buddyai-v2/issues |
| **Discussions** | n/a |
| **Prompt docs / artifacts** | Example deliverables: `project-status-logs/deliverables/` |
