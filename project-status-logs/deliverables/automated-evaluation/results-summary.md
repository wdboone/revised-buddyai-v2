# Results summary (sample format)

The format the evaluation produces. Numbers below are illustrative — they show how results are reported, not a
finding to cite.

## Run configuration

- **Versions compared:** v1 unstructured · v2 fact store · v3 structured · v4 connections
- **Coach:** held constant across versions
- **Judge:** separate model, blind to which version produced each reply, given the full source history as reference
- **Questions:** 12 synthesis probes + 8 advice probes

## Scores (illustrative)

| Version | Synthesis hits (/24) | Advice quality (1–5) |
|---|---|---|
| v1 — unstructured | 14 | 3.6 |
| v2 — fact store | 15 | 3.7 |
| v3 — structured | 17 | 4.0 |
| v4 — connections | 17 | 3.9 |

## How to read it

- **Synthesis hits** count whether the reply reached the buried insight (0/1/2 per probe).
- **Advice quality** rates how well-tailored the guidance was to this specific person.

The comparison the build cares about: does added structure (v1 → v3) buy better coaching, and does
pre-computing connections (v3 → v4) add anything on top? Early signal is that structure helps most when the
coaching model is weaker; a strong model can often infer the connections itself. That directly informs how much
user-modeling machinery Buddy AI needs to build versus letting the model do the work at answer time.
