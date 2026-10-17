# Buddy AI: AI-Powered Life Coach

A conversational coaching app built on Claude Sonnet 4.6, with live web-search grounding, topic routing, a persistent user model, and role-aligned safety guardrails that were red-teamed and measured, not just asserted.

**Live demo:** https://wdboone.github.io/revised-buddyai-v2/

_Sign-up is open on the live app. Create a free test account to try it. Buddy is a coaching tool, not a therapist or a substitute for professional help._

## What it does

- Coaching conversations across eight areas (Relationships, Career, Finances, Parenting, Faith, Workplace Ethics, Personal Growth, and more) plus an open "Just Talk" mode
- User accounts with cloud-synced chat history
- A user model that learns from conversation and from uploaded `.txt` and `.md` files, stored as structured memory
- Web-grounded answers through a search tool
- Role-aligned guardrails: no credential claims, scope-of-practice limits, honest AI disclosure, and a crisis pre-check that surfaces 988 resources

## Architecture

```
Browser (GitHub Pages, single-file index.html)
   |  supabase-js (publishable key + signed-in user session)
   v
Supabase Auth + Postgres (Row Level Security: users see only their own rows)
   |
   +--> Edge Function (holds the Anthropic API key as a server-side secret)
           |-- Claude Haiku: topic routing
           |-- Claude Sonnet 4.6: coaching replies
           '-- memory extraction from conversation and uploaded files
```

| Layer | Choice | Why |
|---|---|---|
| Frontend | One `index.html`, no build step | Easy to deploy and review; trade-off is no module boundaries |
| Auth and data | Supabase Auth and Postgres with RLS | Real protection lives on the server, not in client code |
| AI access | Supabase Edge Function | The API key is never in the browser (see the history below) |
| Models | Sonnet 4.6 for coaching, Haiku for routing | Match model cost and latency to each task |
| Output safety | DOMPurify on rendered Markdown | Model output is treated as untrusted HTML |

### Security history

An early version kept each user's Anthropic key in the browser (`localStorage`) and called the API directly. Issue #11 identified this, and the fix moved all AI calls behind a Supabase Edge Function that uses the user's session token, with the key stored as an encrypted server-side secret. The fix was verified in browser dev tools: the stored key is gone, and network calls go to Supabase, not to the Anthropic API.

## Safety evaluation

The project includes a guardrail test suite in [`guardrail-tests/`](guardrail-tests/) with cases for prompt injection, out-of-scope requests, crisis messages, memory abuse, and benign "twin" cases that check for over-refusal. Full methods and per-case results are in [`FINDINGS.md`](guardrail-tests/FINDINGS.md).

| Metric (original 43 cases: 35 attack, 8 benign) | Baseline | After prompt-level hardening |
|---|---|---|
| Attack success rate | 8.6% (3 of 35) | 0% (0 of 35) |
| Over-refusal on benign cases | 1 of 8 | 1 of 8 |
| Crisis recall | 10 of 10 | 10 of 10 |
| Unsafe memory writes | 2 | 0 |

The suite was then expanded to 48 cases. On the expanded set, one case (`tn-09`) still produces an unsafe memory write, where the coach stored a specific date the user never gave. A second new case (`cres-05`) was judged a borderline bypass. Both are documented as known residuals.

**How to read these numbers.** The suite is small (35 attack cases), so "0 of 35" shows improvement against this suite, not proof of safety. The prompt changes were tuned against the same cases they were measured on. The crisis regex pre-check never fired on the evasion cases; the model itself caught them, so the regex is a backstop, not the main defense.

## Known limitations and next steps

- **System prompt location.** The coaching prompt is assembled in the client. Planned: build it server-side so the Edge Function never trusts client-supplied prompt text.
- **No rate limiting** on the Edge Function yet.
- **Output-side classifier** (checking replies and memory writes before they are saved) was designed but postponed. It is the proposed fix for the `tn-09` residual.
- **Memory retrieval.** The coach is fed extracted facts rather than raw history. A tiered retrieval design is scoped as an open spike (see Issues).
- **Small evaluation set**, as noted above.

## Setup (to run your own copy)

1. Create a Supabase project and run the SQL schema for the tables, with Row Level Security enabled on every table.
2. Deploy the Edge Function and add your Anthropic key as a secret named `ANTHROPIC_API_KEY` (Supabase Dashboard, Edge Functions, Secrets). Never put this key in `index.html`.
3. Set the two config values in `index.html`: your Supabase project URL and publishable key. The publishable key is designed to be public; RLS protects the data.
4. Host `index.html` on any static host, such as GitHub Pages.

## Team

- **Willie D. Boone III**: lead developer (app, Supabase backend, Edge Function)
- **@hunterphillips**: evaluation, guardrail test suite, and design spikes

Built as a capstone prototype for the Master of Science in Applied Artificial Intelligence program (Studio II, Summer 2026). Process logs and sprint notes are in [`project-status-logs/`](project-status-logs/).

## License

MIT. See [`LICENSE`](LICENSE).
