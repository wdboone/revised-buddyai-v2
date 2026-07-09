# Self-interview instrument

The instrument used to collect persona data — the material the user-model versions are built from. An AI runs a
structured self-interview: the subject talks about their own life, the AI draws it out.

The design goal is **even coverage over depth**. Rather than following one thread as far as it goes, the
interview works across a grid of life domains, collecting a few concrete, dated scenes in each. That breadth is
what lets the more structured user-model versions differ from the flat ones — thin, uneven data collapses the
distinction.

This revision (Sprint 1) shifted the instrument from open-ended interviewing to this structured, fact-gathering
stance, after open-ended sessions produced commentary instead of usable material.

## What's here

| File | What it is |
|---|---|
| `interviewer-brief.md` | The operating manual for the AI running the interview. |
| `theme-bank.md` | The grid of life domains to cover, each with prompts and a stop condition. |

The instrument only; the persona data it collects is kept out of this repo.
