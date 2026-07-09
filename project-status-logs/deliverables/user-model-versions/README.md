# Four user-model design versions

Four ways the app could represent the same user, each adding one capability to the version before it. The
question is whether more structure produces better coaching, and where the payoff stops being worth the cost.

All four describe the same fictional person (Dana Whitfield) so the versions can be compared directly. Only the
*representation* changes.

| Version | What it is | File |
|---|---|---|
| **v1 — Unstructured** | A plain-prose summary of the person. The simplest baseline. | `v1-unstructured.md` |
| **v2 — Fact store** | The same information broken into discrete, individually-stored facts, each tagged with confidence and whether it's durable or temporary. | `v2-fact-store.jsonl` |
| **v3 — Structured** | The facts organized into three layers: stable **traits**, current **concerns**, and the life **story**. (Based on a three-level model of personality from psychology — McAdams.) | `v3-structured/` |
| **v4 — Connections** | Everything in v3, plus explicit **cross-cutting patterns** that link facts across the three layers into conclusions no single fact states. | `v4-connections.md` |

Each step is one comparison: v1 → v2 tests structure vs. prose, v2 → v3 tests organized vs. flat, and
v3 → v4 tests whether pre-computing the connections helps beyond just having the organized facts.
