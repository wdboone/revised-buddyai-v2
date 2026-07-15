# Results summary (sample format)

The format the evaluation produces. Numbers below are illustrative. They show how results are reported, not a
finding to cite.

## Run configuration

- **Versions compared:** raw · faceted · connected
- **Coach:** held constant across versions; three blind coaches per question
- **Judge:** separate model, blind to which version produced each reply, given the full source history as reference; plus a human pass where the subject rates replies about their own life
- **Questions:** the discriminating set, with synthesis scored per reply

## Scores (illustrative)

| Version | Synthesis (avg) | Advice quality (1–5) | Best-reply picks |
|---|---|---|---|
| raw | 4.2 | 4.3 | 5 |
| faceted | 3.8 | 3.9 | 0 |
| connected | 3.9 | 4.0 | 1 |

## How to read it

- **Synthesis** rates whether the reply reached an insight no single stored sentence states.
- **Advice quality** rates how well-tailored the guidance was to this person.
- **Best-reply picks** count the questions where the judge (or subject) named that version's reply the best.

The comparison the build cares about: does arranging the user model into structure improve the coaching? With
information held identical across versions, the raw history came out on top, and the human subject preferred it
clearly. Arranging the facts, and pre-computing the connections, did not improve the advice. That informs how
much user-modeling machinery Buddy AI needs versus feeding the coach the raw history while it fits in context.
