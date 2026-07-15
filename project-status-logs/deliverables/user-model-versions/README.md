# User-model design versions

Three ways the app could represent the same user, built so they hold identical information and differ only in
how it's arranged. Same person (fictional: Dana Whitfield) in each. The question is whether arranging the user
model into structure improves the coaching the app produces.

| Version | What it is | File |
|---|---|---|
| **Raw** | The user's history as plain prose. The baseline. | `raw.md` |
| **Faceted** | The same sentences from the raw history, sorted into three layers — stable **traits**, active **concerns**, and the **story** over time. Nothing is reworded. | `faceted/` |
| **Connected** | Everything in faceted, plus a layer of explicit **connections** that link facts across the three layers into conclusions no single sentence states. | `connected.md` |

## Lossless by design

The versions differ only in arrangement. The faceted version reuses the raw history's exact sentences, just
sorted into layers, and the connected version adds a layer without removing anything. Because every version
carries the same information, a difference in coaching quality is attributable to the arrangement alone.

An earlier design included a fourth "extracted fact store" version. It was dropped: producing it meant rewriting
the history into terse facts, which lost concrete detail and confounded the comparison. Sorting keeps the words;
extraction changes them.

## What the comparison tests

Raw → faceted tests whether layering the user model helps. Faceted → connected tests whether pre-computing the
cross-layer connections helps beyond having the sorted facts.
