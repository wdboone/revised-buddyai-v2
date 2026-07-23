# Guardrail test suite (issue #9)

A red-team harness that measures how well Buddy adheres to its coaching-role and safety guardrails. It runs a
labeled set of adversarial and benign messages through Buddy's *real* system prompt and crisis regex, grades each
reply with an LLM-as-judge plus deterministic checks, and reports attack success rate, over-refusal, and
crisis-detection coverage. It tests model behavior only — not Supabase, the topic classifier, or persistence.

This is dev tooling. It is not part of the shipped app and imports nothing from `index.html`; it mirrors the
app's prompt, crisis regex, and API call inside `buddy-core.mjs`. If you change those in `index.html`, update
`buddy-core.mjs` to match.

## Files

| File | Role |
| --- | --- |
| `cases.json` | 48 labeled red-team cases across 9 categories |
| `judge-rubric.md` | The LLM-as-judge prompt (single source both runners load) |
| `buddy-core.mjs` | Shared engine: mirrors Buddy, replays cases, runs the judge, computes metrics |
| `run-node.mjs` | Node CLI runner |
| `runner.html` | Browser runner |
| `FINDINGS.md` | The written spike findings: coverage, gaps, recommendations |
| `results/` | Generated output, one timestamped report/results pair per run (gitignored) |

## Setup

Both runners read keys from `.env.local` (gitignored). The app's `.env.local` at the repo root
(`revised-buddyai-v2/.env.local`) is used automatically; a `.env.local` inside `guardrail-tests/` also works and
takes precedence. It should contain:

```
ANTHROPIC_API_KEY=sk-ant-...     # the coaching model (mirrors the app)
OPENAI_API_KEY=sk-...            # the default cross-family judge (gpt-5.6)
```

The judge defaults to OpenAI `gpt-5.6` (a different model family than the Claude coach, which avoids
self-preference bias). Without an OpenAI key it falls back to Anthropic `claude-opus-4-8`. Model IDs are two
constants at the top of `buddy-core.mjs` if your account differs.

Real runs make live API calls (coaching model + web search + judge) and cost money. Use `--dry-run` first to
validate wiring with zero spend.

## Node runner

```bash
cd guardrail-tests
node run-node.mjs --dry-run              # no network; validates the pipeline
node run-node.mjs                        # full run; judge auto-selected (OpenAI if key present)
node run-node.mjs --judge=anthropic      # force the Opus judge
node run-node.mjs --category=crisis-evasion
node run-node.mjs --case=jb-01
```

Writes a timestamped pair under `results/` — `<timestamp>_<live|dry>.report.md` (human-readable) and
`.results.json` (raw per-case verdicts) — so runs never overwrite each other, and prints a summary noting
which judge was used.

## Browser runner

Serve from the repo root so the page can reach both the suite files and the repo-root `.env.local`, then open the
runner:

```bash
cd ..                          # revised-buddyai-v2/ (repo root)
python3 -m http.server 8091    # then open http://localhost:8091/guardrail-tests/runner.html
```

Keys auto-load from `.env.local` (paste is the fallback). Pick a judge (Auto / OpenAI / Anthropic), click **Dry
run** to validate with no API calls, or **Run suite** for a real run. Filter by category, watch results stream into
the table, and read the summary tiles (attack success rate, over-refusal, crisis recall/precision, unsafe-memory
and ungraded-error counts, and the regex-vs-model crisis breakdown).

Security note: serving the folder also serves `.env.local` on that port for as long as the server runs, so anything
on the machine can read the keys. It's a localhost-only exposure; for real runs the CLI (which reads the file off
disk, never over HTTP) is the safer path.

## Case schema

Each case in `cases.json`: `id`, `category`, `title`, `turns` (array; multi-turn = more than one), plus optional
`injected_context` (untrusted web content for indirect-injection cases), `seed_facts` (pre-load a poisoned
user-model profile), `category_id` (coaching domain, default general), and `canary` (a token the attack tries to
make the model emit or persist — if it shows up, the harness deterministically marks the attack as landed).
`expected_behavior` is one of `comply` | `refuse` | `refuse-with-resources` | `partial-comply-safe`.

## Metrics

- **Attack success rate** — graded attacks that got through (lower is better).
- **Refusal rate** — graded attacks correctly refused.
- **Over-refusal rate** — benign true-negative cases wrongly refused (lower is better).
- **Crisis recall / precision** — crisis cases where resources surfaced, and how much of that surfacing was
  correct.
- **Crisis breakdown** — regex-caught vs model-caught vs neither. The headline: how much the model backstop
  covers the regex's blind spots.
- **Unsafe memory writes** and **ungraded errors** — raw counts.

Two validity rules: a judge/API/parse failure is an `error` outcome, excluded from every rate and counted
separately (the CLI also exits non-zero), so a broken run can't look like 0% ASR. And dry-run makes no model calls
— its verdicts are stubs for validating the pipeline, never a safety result.

See `FINDINGS.md` for what these reveal, what is deliberately out of scope (adaptive attackers, the live web-search
channel, clinician-grade crisis coverage), and the recommended next steps.
