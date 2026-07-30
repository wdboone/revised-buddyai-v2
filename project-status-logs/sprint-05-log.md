# MSAI 5573 · AI Studio II — Team Weekly Sprint Log

## 1. Sprint information

| | |
|---|---|
| **Project / Team** | Buddy AI — AI-powered life coach |
| **Sprint number** | Sprint 5 |
| **Week of (start – end)** | 07/28/2026 – 08/03/2026 |
| **Sprint goal (one sentence)** | Finish the end-of-term presentation and clear the remaining auth UX gaps. |
| **Facilitator / scribe** | Hunter Phillips |
| **Members present** | Hunter Phillips, Willie Boone |
| **Members absent** | None |

## 2. Standup round-robin

| Team member | Done since last standup | Plan before next standup | Blockers / help needed |
|---|---|---|---|
| Willie Boone | Filled his sections of the final presentation (#14): condensed team-slide bullets, embedded the live deployed app in the demo slide with an open-in-new-tab fallback, and wrote his learning outcomes. | Confirm the deck review is complete and close #14; help verify the password-reset email round-trip on the live site. | None. |
| Hunter Phillips | Documented the hardened guardrails in the README; built the final presentation deck and the guardrail demo deck (real before/after transcripts, harness walkthrough, prompt diff); found and fixed two auth dead-ends — no password reset, and signup with an existing email waiting forever on a confirmation email (#15, closed); opened the tiered-memory spike (#13). | Write the remaining learning-outcomes bullets; rehearse the demo including the embedded live app; verify the reset-email round-trip; start #13 if time allows. | None. |

## 3. Board snapshot (GitHub Project)

| Date | Backlog | Ready | In Progress | In Review | Done | Notes |
|---|---|---|---|---|---|---|
| 07/30 | Tiered memory spike (#13) | | | | Auth UX fix (#15); Deck review (#14); Final presentation content | #15 opened, implemented, reviewed, closed, and verified live same week. #14 closed with Willie's sections in. Issues: https://github.com/wdboone/revised-buddyai-v2/issues |

## 4. Blockers & risks

| Blocker / risk | Impact | Owner | Action to resolve | Status |
|---|---|---|---|---|
| The password-reset email leg is code-reviewed but untested against the real Supabase project. | A broken reset flow would recreate the lockout it was built to fix. | Hunter / Willie | Verified live 07/30: reset requested, emailed link followed, new password set, landed in the app. | Resolved |
| The presentation's demo depends on the live app inside an iframe; login may misbehave cross-origin. | A stalled demo in front of the class. | Hunter | Rehearse beforehand; the open-in-new-tab link is the fallback. | Open |
| The `chat` Edge Function source is still not in the repo (carried from Sprint 4). | The deployed safety-critical proxy isn't version-controlled. | Willie | Pull the function source into the repo. | Open |

## 5. Decisions made

| Decision | Why | Owner | Date |
|---|---|---|---|
| Demo the live deployed app embedded in the presentation, with an open-in-new-tab fallback. | Shows the real product rather than screenshots; the fallback covers iframe login issues. | Willie | 07/28 |
| Password-reset messaging is enumeration-safe ("If an account exists for that email…"), matching Supabase's own anti-enumeration signup behavior. | The signup flow already refuses to reveal whether an email is registered; the reset flow shouldn't leak it either. | Hunter | 07/30 |

## 6. Action items & next steps

| Action / next step | Owner | Due | Link (PR / issue / story) |
|---|---|---|---|
| ~~Write the remaining learning-outcomes bullets on the closing slide~~ Done 07/30. | Hunter | Done | https://github.com/wdboone/revised-buddyai-v2/issues/14 |
| ~~Close #14~~ Closed 07/30 with Willie's sections in. | Willie | Done | https://github.com/wdboone/revised-buddyai-v2/issues/14 |
| ~~Live round-trip test of the password-reset flow~~ Done 07/30: verified on the live site. | Hunter | Done | https://github.com/wdboone/revised-buddyai-v2/issues/15 |
| Tiered memory retrieval spike. | Hunter | Open | https://github.com/wdboone/revised-buddyai-v2/issues/13 |
| Pull the `chat` Edge Function source into the repo (carried from Sprint 4). | Willie | Next standup | https://github.com/wdboone/revised-buddyai-v2/issues/9 |

## 7. Sprint reflection

| Reflection prompt | Team's notes |
|---|---|
| **What went well this sprint?** | The presentation came together with both members' sections in place, and a real UX bug — found by getting locked out of an account — went from discovery to filed, fixed, reviewed, and shipped in a day. |
| **What slowed us down?** | The auth dead-end itself: being unable to reset a password or learn that an account already existed cost real time before it was diagnosed as the app's gap rather than user error. |
| **What will we change next sprint?** | Rehearse the demo path end-to-end before presenting instead of trusting that the deployed app will behave inside the deck. |

## 8. Links & artifacts

| | |
|---|---|
| **GitHub repository** | https://github.com/wdboone/revised-buddyai-v2 |
| **GitHub Project board** | https://github.com/wdboone/revised-buddyai-v2/issues |
| **Discussions** | n/a |
| **Prompt docs / artifacts** | Guardrail suite: `guardrail-tests/`; final presentation: `project-status-logs/final-presentation.html`; example deliverables: `project-status-logs/deliverables/` |
