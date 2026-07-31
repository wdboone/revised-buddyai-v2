# MSAI 5573 · AI Studio II — Individual Sprint Log (Willie Boone)

## 1. Sprint information

| | |
|---|---|
| **Project / Team** | Buddy AI — AI-powered life coach |
| **Sprint number** | Sprint 5 |
| **Week of (start – end)** | 07/28/2026 – 08/03/2026 |
| **Team sprint goal** | Finish the end-of-term presentation and clear the remaining auth UX gaps. |
| **My focus this sprint** | Complete my sections of the final presentation and support final verification. |

## 2. My standup answers

| | |
|---|---|
| **Done since last standup** | Filled my sections of the final presentation (#14): condensed my team-slide bullets to match the deck's format, embedded the live deployed app directly into the demo slide with an open-in-new-tab fallback for reliability, and wrote my closing learning-outcome reflections. |
| **Plan before next standup** | Confirm the deck review is complete and close #14; help verify the password-reset email round-trip on the live site. |
| **Blockers / help needed** | None. |

## 3. Board snapshot

See the team sprint log (`sprint-05-log.md`) for the shared board snapshot as of 07/30.

## 4. Blockers & risks I owned

| Blocker / risk | Impact | Status |
|---|---|---|
| The `chat` Edge Function source is still not in the repo (carried from Sprint 4). | The deployed safety-critical proxy isn't version-controlled. | Open — pull the function source into the repo |
| The presentation's live demo runs inside an iframe; login may misbehave cross-origin. | A stalled demo in front of the class. | Open (Hunter's risk to manage during rehearsal) — the open-in-new-tab link I added is the fallback |

## 5. Decisions I made or contributed to

| Decision | Why | Date |
|---|---|---|
| Demo the live deployed app embedded in the presentation, with an open-in-new-tab fallback. | Shows the real product rather than screenshots; the fallback covers iframe login issues. | 07/28 |

## 6. Action items & next steps

| Action / next step | Status | Link |
|---|---|---|
| Close #14 with my sections in. | Done 07/30 | github.com/wdboone/revised-buddyai-v2/issues/14 |
| Pull the `chat` Edge Function source into the repo (carried from Sprint 4). | Still open | github.com/wdboone/revised-buddyai-v2/issues/9 |

## 7. My sprint reflection

**What went well:** My sections of the final presentation came together cleanly — the demo slide in particular, since embedding the live app directly rather than screenshots makes a much stronger case in front of the class.

**What slowed me down:** Nothing blocking on my end this sprint.

**What I'll change next time:** Actually rehearse the live-demo path end-to-end before presenting, rather than assuming the deployed app will behave correctly inside the deck on the first real attempt — this was the team's shared reflection this sprint, and it applies directly to the slide I built.

## 8. Note on this sprint's record

Hunter's team sprint log credits him with building the final presentation deck itself, the separate guardrail demo deck, and the full speaker guide and presentation-day cheat sheet for the HTML version this sprint. My own contribution was specifically my two content sections (#14) and demo-slide integration — this log reflects that division accurately rather than the broader authorship an earlier draft of my Activity Log implied.

## 9. Links & artifacts

| | |
|---|---|
| **GitHub repository** | https://github.com/wdboone/revised-buddyai-v2 |
| **Deliverable(s) this sprint** | Final presentation (HTML) — Slide 2 content (Willie profile) and Slide 8 content (Willie closing learnings); demo-slide live-app embed with fallback link |
