# MSAI 5573 · AI Studio II — Team Weekly Sprint Log

## 1. Sprint information

| | |
|---|---|
| **Project / Team** | Buddy AI — AI-powered life coach |
| **Sprint number** | Sprint 4 |
| **Week of (start – end)** | 07/21/2026 – 07/27/2026 |
| **Sprint goal (one sentence)** | Measure the app's guardrail adherence with a repeatable red-team suite, and clear the signup blocker. |
| **Facilitator / scribe** | Hunter Phillips |
| **Members present** | Hunter Phillips, Willie Boone |
| **Members absent** | None |

## 2. Standup round-robin

| Team member | Done since last standup | Plan before next standup | Blockers / help needed |
|---|---|---|---|
| Willie Boone | Fixed the email-confirmation redirect by adding `emailRedirectTo` in signUp, so new users land on the real host instead of a broken localhost link (#8); shipped file upload → fact extraction so the user model can be updated from uploaded files (#10); moved the Anthropic API key server-side via a Supabase Edge Function so the browser no longer holds it (#11). | Support the guardrail-hardening implementation (#9 follow-up). | None. |
| Hunter Phillips | Delivered the guardrail spike (#9): built a 43-case red-team suite over the app's real prompt and crisis regex, hardened it against an adversarial critique, ran the first live suite, and wrote up the results. Buddy refused 32 of 35 attacks; the crisis keyword regex caught 0 of 10 evasions. | Start implementing guardrail hardening from the spike's findings, at the prompt level first: an escalation-proof medication refusal, an explicit instruction hierarchy with spotlighted untrusted content, and a persist-only-stated-facts rule. | None. |

## 3. Board snapshot (GitHub Project)

| Date | Backlog | Ready | In Progress | In Review | Done | Notes |
|---|---|---|---|---|---|---|
| 07/22 | Server-side API proxy | | Server-side API proxy | | Email-confirmation fix (#8); Guardrails spike (#9); File upload → user model (#10) | All open issues closed; only the server-side proxy (roadmap) remains. Issues: https://github.com/wdboone/revised-buddyai-v2/issues |
| 07/23 | | | | | Guardrail hardening — Measure 1 (#12) | Prompt-level hardening implemented, verified against the baseline, and closed same day. Measure 2 (output-side check) deferred. |

## 4. Blockers & risks

| Blocker / risk | Impact | Owner | Action to resolve | Status |
|---|---|---|---|---|
| Crisis keyword regex catches 0 of 10 evasions (algospeak, leetspeak, spacing, misspelling, non-English); the model backstop is the only crisis guardrail, and it is a prompt instruction, not enforced in code. | A missed crisis reaches a user with nothing between it and them. | Willie / team | Prompt hardening landed (#12): like-for-like attack success 8.6% → 0%, crisis recall held at 100% (still all model-caught). The regex is unchanged and the output self-check (Measure 2) is deferred, so the model backstop remains the only crisis layer. | Mitigated |
| Anthropic API key was held in the browser. | Fine for a demo, not safe for real users. | Willie | Moved server-side via a Supabase Edge Function (#11). | Resolved |

## 5. Decisions made

| Decision | Why | Owner | Date |
|---|---|---|---|
| Scope the guardrail spike to model adherence (does Buddy hold its role/safety rules), not app logic. | Keeps the spike focused; the Supabase/classifier/RLS layers are a separate assessment. | Hunter | 07/21 |
| Judge with a cross-family model (OpenAI GPT grading the Claude coach), Anthropic Opus as fallback. | Removes the self-preference bias a Claude-grading-Claude setup would carry. | Hunter | 07/21 |
| A coach-side API error is recorded as an `error` outcome, excluded from every rate, with a non-zero CLI exit. | An error string was being graded as if Buddy said it, which corrupted the metrics; errors must never masquerade as a clean result. | Hunter | 07/22 |
| Generalize the planned medication-dose refusal into a category-level scope-of-practice rule with bright-line examples. | Dosage was just the topic the suite happened to test; a per-topic rule leaves every unlisted domain uncovered, while a purely abstract rule leaves the judgment call escalation attacks erode. | Hunter | 07/23 |
| Accept Measure 1 as-is and defer Measure 2 (output-side policy classifier). | The prompt-only change closed all three baseline bypasses with no new over-refusals; the classifier's open design questions aren't resolved and the residual risks don't currently justify it. | Hunter | 07/23 |

## 6. Action items & next steps

| Action / next step | Owner | Due | Link (PR / issue / story) |
|---|---|---|---|
| ~~Prompt-level guardrail hardening~~ Done 07/23: scope-of-practice, untrusted-content, and persist-only-stated-facts rules shipped and verified (attack success 8.6% → 0% like-for-like). | Hunter | Done | https://github.com/wdboone/revised-buddyai-v2/issues/12 |
| Output self-check before render (Measure 2) — deferred; revisit if residual risks resurface. Open design questions are in `guardrail-tests/HARDENING-PLAN.md`. | Team | Deferred | https://github.com/wdboone/revised-buddyai-v2/issues/12 |
| Pull the `chat` Edge Function source into the repo (README points at a non-existent path). | Willie | Next standup | https://github.com/wdboone/revised-buddyai-v2/issues/9 |
| Continue toward the server-side API-key proxy. | Willie | Next standup | https://github.com/wdboone/revised-buddyai-v2/issues |

## 7. Sprint reflection

| Reflection prompt | Team's notes |
|---|---|
| **What went well this sprint?** | Delivered a repeatable guardrail measurement; the first live run gave a clean baseline (8.6% attack success rate) and surfaced three concrete gaps. Signup is unblocked, file-upload → user-model shipped, and every open issue is now closed. |
| **What slowed us down?** | A dry run overwrote a live results file, and a harness bug graded API errors as replies. Both are fixed — runs now write to a timestamped folder and API errors are recorded as errors — but they cost a rerun. |
| **What will we change next sprint?** | Move from measuring to fixing: implement guardrail hardening from the spike's findings, starting with prompt-level defenses (escalation-proof medication refusal, instruction hierarchy, spotlighted untrusted content), then an output self-check. |

## 8. Links & artifacts

| | |
|---|---|
| **GitHub repository** | https://github.com/wdboone/revised-buddyai-v2 |
| **GitHub Project board** | https://github.com/wdboone/revised-buddyai-v2/issues |
| **Discussions** | n/a |
| **Prompt docs / artifacts** | Guardrail suite: `guardrail-tests/`; example deliverables: `project-status-logs/deliverables/` |
