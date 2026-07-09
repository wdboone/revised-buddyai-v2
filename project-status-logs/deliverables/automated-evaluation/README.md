# Automated evaluation

How the four user-model versions are compared. The setup is a controlled test: the coaching prompt and the
questions are held identical across all four versions, and only the user-model context changes. Whatever
difference shows up in the coaching replies is attributable to the representation.

## How it runs

1. For each version, feed the coach the **same coaching prompt** plus **that version's user-model**.
2. Send the coach the **same set of user messages** (the evaluation questions).
3. Collect the coaching replies.
4. A separate judge scores each reply against the question's target, without knowing which version produced it.

## What's here

| File | What it is |
|---|---|
| `coaching-prompt.md` | The instructions given to the coach, identical for every version. |
| `evaluation-questions.md` | Sample user messages, split into synthesis probes and advice probes. |
| `results-summary.md` | A sample of the results format the run produces. |

## What it measures

- **Synthesis** — does the reply reach an insight that no single stored fact states, requiring facts to be
  connected across the person's history?
- **Advice quality** — is the advice genuinely tailored to this person, or generic enough to send to anyone?
