# Activity & Deliverables Log — Hunter Phillips

Running progress record + mid-term assessment summary.

## Student & Project Information

| | |
|---|---|
| **Student name** | Hunter Phillips |
| **Cohort (Fall / Spring / Summer)** | Spring |
| **Course (Studio I / II)** | Studio II |
| **Project / client** | Buddy AI — AI-powered life coach (AI coaching application) |
| **Team members** | Willie Boone (lead dev), Hunter Phillips (research informing the build direction; architecture guidance & testing) |
| **Professor** | Diaz |

## Weekly Standup Notes

| Week / Date | Done since last standup | Planned before next standup | Blockers, risks & decisions |
|---|---|---|---|
| Wk 1 · 06/30 | Built the four user-model versions from the evaluation persona; authored the evaluation question sets and coaching prompt; revised the self-interview instrument; began collecting the personal persona dataset; gave architecture feedback on the initial prototype. | Finish the personal persona dataset; run the evaluation across the four versions; begin building user models from the personal dataset. | Blocker: gathering personal data is slow. Decision: switched persona collection to a structured, fact-gathering questionnaire. |
| Wk 2 · 07/07 | Finished the personal persona dataset; upgraded and ran the automated evaluation across the four versions and recorded the first results; began building the four user-model versions from the personal dataset; reviewed the new demo app. | Finish building the four versions on the personal dataset; run the evaluation on them; fold the findings into the build's user-modeling approach. | Decision: dropped simple recall questions from the evaluation to focus on synthesis and advice. |

## Activity Log

| Date | Wk | Activity — what you did | Deliverable(s) it created or advanced | Your role | Status / hrs | URL (PR / board / doc) |
|---|---|---|---|---|---|---|
| 06/30 | 1 | Prepared a clean evaluation dataset from a public writing archive to serve as a realistic test persona for the user-modeling work. | Evaluation dataset (test persona) | Created | Done · 0.5h | Research informing the build |
| 06/30 | 1 | Built four increasingly structured versions of the app's user-model design — from an unstructured summary up to a richly connected person-model — to compare how the way the app represents a user affects coaching quality. | Four user-model design versions | Created | Done · 1.25h | [example](deliverables/user-model-versions/) |
| 06/30 | 1 | Authored a set of evaluation questions that probe how well each version supports insight and synthesis about the user. | Evaluation question set | Created | Done · 0.5h | [example](deliverables/automated-evaluation/) |
| 06/30 | 1 | Reviewed the initial Buddy AI prototype/mockup and gave architecture guidance and feedback. | Prototype architecture feedback | Reviewed | Done · 0.5h | https://github.com/wdboone/revised-buddyai-v2 |
| 07/01 | 1 | Authored the advice-focused evaluation questions and the coaching prompt that drive the automated evaluation. | Evaluation questions + coaching prompt | Created | Done · 0.5h | [example](deliverables/automated-evaluation/) |
| 07/02 | 1 | Revised the self-interview instrument used to gather persona data, shifting it to structured, broad-coverage fact-gathering. | Self-interview instrument (revised) | Created | Done · 0.5h | [example](deliverables/self-interview-instrument/) |
| 07/02–07/06 | 1 | Collected a personal persona dataset through structured self-interviews, to serve as the primary evaluation case for the user-modeling work. | Personal persona dataset | Created | In progress · 1h | Research informing the build |
| 07/06 | 1 | Finalized the revised intake questionnaire for pure fact-gathering. | Intake questionnaire (final) | Created | Done · 0.25h | Research informing the build |
| 07/07–07/08 | 2 | Finished the personal persona dataset: added the supporting documents (background, values, personality assessments) and consolidated the interview transcripts into one curated source. | Personal persona dataset | Created | Done · 1.5h | Research informing the build |
| 07/08 | 2 | Upgraded the automated evaluation: set the coach to a mid-tier model, added an independent judge that grades each reply against the full source history, and tightened the scoring so unsupported claims can't score well. | Automated evaluation (upgraded) | Created | Done · 1.5h | [example](deliverables/automated-evaluation/) |
| 07/08 | 2 | Ran the evaluation across the four user-model versions and recorded the first results. | Evaluation results | Created | Done · 1h | [example](deliverables/automated-evaluation/) |
| 07/08 | 2 | Trimmed the evaluation question suite to synthesis and advice questions, dropping simple recall. | Evaluation question set (revised) | Created | Done · 0.5h | [example](deliverables/automated-evaluation/) |
| 07/09 | 2 | Began building the four user-model versions from the personal persona dataset (the primary evaluation case). | Four user-model design versions (personal dataset) | Created | In progress · 1h | [example](deliverables/user-model-versions/) |
| 07/09 | 2 | Reviewed the new Buddy AI demo app and its added features, and gave architecture guidance and feedback. | Demo app architecture feedback | Reviewed | Done · 0.5h | https://github.com/wdboone/revised-buddyai-v2 |

## Deliverables Register

| Deliverable | Type | Your role | Your specific contribution | Status | Link / location |
|---|---|---|---|---|---|
| Four user-model design versions (evaluation persona) | Research artifacts | Created | Built four increasingly structured ways for the app to represent a user, so the team can choose a user-modeling approach for the build from evidence rather than guesswork. | Complete | [`deliverables/user-model-versions/`](deliverables/user-model-versions/) |
| Automated evaluation (questions + coaching prompt) + first results | Research artifacts | Created | Authored the questions and coaching prompt, rebuilt the evaluation with an independent history-grounded judge and stricter scoring, ran it across the four versions, and recorded the results. | Complete | [`deliverables/automated-evaluation/`](deliverables/automated-evaluation/) |
| Self-interview instrument (revised) | Docs | Created | Rewrote the instrument for structured, broad-coverage fact-gathering instead of open-ended interviewing. | Complete | [`deliverables/self-interview-instrument/`](deliverables/self-interview-instrument/) |
| Personal persona dataset | Dataset | Created | Collected structured self-interviews and supporting documents into a curated dataset — the primary evaluation case. | Complete | Research informing the build |
| Four user-model versions (personal dataset) | Research artifacts | Created | Started building the four representations from the personal dataset, to test the design on the primary evaluation case. | In progress | [`deliverables/user-model-versions/`](deliverables/user-model-versions/) |
| Buddy AI prototype/demo architecture & feedback | Review | Reviewed | Gave architecture guidance and feedback on the initial prototype and the later demo app. | Ongoing | https://github.com/wdboone/revised-buddyai-v2 |

## Mid-Term Summary (this is what you submit)

_To be assembled from the logs above at the checkpoint._
