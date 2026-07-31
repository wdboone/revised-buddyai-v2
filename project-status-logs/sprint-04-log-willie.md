# MSAI 5573 · AI Studio II — Individual Sprint Log (Willie Boone)

## 1. Sprint information

| | |
|---|---|
| **Project / Team** | Buddy AI — AI-powered life coach |
| **Sprint number** | Sprint 4 |
| **Week of (start – end)** | 07/21/2026 – 07/27/2026 |
| **Team sprint goal** | Measure the app's guardrail adherence with a repeatable red-team suite, and clear the signup blocker. |
| **My focus this sprint** | Clear the three open production/security issues and support the guardrail-hardening rollout. |

## 2. My standup answers

| | |
|---|---|
| **Done since last standup** | Fixed the email-confirmation redirect by adding `emailRedirectTo` in `signUp()`, so new users land on the real host instead of a broken localhost link (#8). Shipped file upload → fact extraction so the user model can be updated directly from uploaded files (#10). Moved the Anthropic API key server-side via a Supabase Edge Function so the browser no longer holds it (#11). Also designed and built the capstone presentation framework (33+ slides) with detailed speaker notes and a presentation-day quick reference guide, as a backup deliverable format. |
| **Plan before next standup** | Support the guardrail-hardening implementation (#9 follow-up); finalize presentation materials. |
| **Blockers / help needed** | None. |

## 3. Board snapshot

See the team sprint log (`sprint-04-log.md`) for the shared board snapshot as of 07/22 and 07/23.

## 4. Blockers & risks I owned

| Blocker / risk | Impact | Status |
|---|---|---|
| Anthropic API key was held in the browser | Fine for a demo, not safe for real users | Resolved — moved server-side via Supabase Edge Function (#11) |
| Crisis keyword regex catches 0 of 10 evasions (Hunter's red-team finding); the model backstop is the only crisis guardrail | A missed crisis reaches a user with nothing between it and them | Mitigated by Hunter's prompt hardening (#12) — I supported verification but the fix and the finding were his |

## 5. Decisions I made or contributed to

None this sprint that I owned individually — the guardrail-related decisions (spike scope, judge design, error handling, the generalized scope-of-practice rule, and deferring Measure 2) were Hunter's, made and documented in his research track.

## 6. Action items & next steps

| Action / next step | Due | Link |
|---|---|---|
| Pull the `chat` Edge Function source into the repo (README points at a non-existent path). | Sprint 5 | github.com/wdboone/revised-buddyai-v2/issues/9 |
| Continue toward finalizing the server-side API-key proxy. | Sprint 5 | github.com/wdboone/revised-buddyai-v2 |

## 7. My sprint reflection

**What went well:** Cleared all three of my open issues (#8, #10, #11) in one sprint, and the API key is finally off the browser for good — the last significant client-side security gap in the app.

**What slowed me down:** Nothing blocking on my side. The bigger sprint-level slowdown was on Hunter's evaluation harness, not my application work.

**What I'll change next sprint:** Get the `chat` Edge Function source into the repo — it's been deployed and safety-critical since this sprint, but it's still not version-controlled, which I flagged but didn't close out.

## 8. Links & artifacts

| | |
|---|---|
| **GitHub repository** | https://github.com/wdboone/revised-buddyai-v2 |
| **Deliverable(s) this sprint** | Signup confirmation-email fix (#8); file upload → user model (#10); server-side API-key proxy via Edge Function (#11); Buddy AI capstone presentation framework (PowerPoint); presentation speaker guide and cheat sheet |
