# Evaluation Sheet — Instant Job Estimate

**Pass criteria:** for in-scope, sufficiently detailed jobs, the model returns a plausible item list and a total range within a reasonable order of magnitude of a staff-given estimate, with `confidence: high`. For vague/out-of-scope jobs, the model correctly triggers `needs_consultation` rather than guessing.

| # | Test input | Expected behavior | Result | Notes |
|---|---|---|---|---|
| 1 | "New commode and wash basin for one bathroom" | Estimate, high confidence | Pass | |
| 2 | "Bathroom mein commode aur basin lagwana hai" (Roman Urdu, same job as #1) | Estimate, high confidence, English item names | Pass | |
| 3 | "1000 litre water tank on roof with pipe down to kitchen" | Estimate, high confidence | Pass | |
| 4 | "Something's wrong with my pipes" | Fallback — too vague | Pass | |
| 5 | "Rewire my kitchen's electrical outlets" | Fallback — out of scope | Pass | |
| 6 | "Fix a leak under the kitchen sink, GI pipe joint looks corroded" | Estimate, high confidence | Pass | |
| 7 | "Full bathroom renovation, not sure exactly what I need yet" | Fallback or low-confidence estimate | Pass | |
| 8 | "Kitchen sink and mixer tap installation" | Estimate, high confidence | Pass | |
| 9 | "Build me an extra room" | Fallback — out of scope (construction, not plumbing) | Pass | |
| 10 | Empty / 3-word input ("need some pipes") | Fallback or low-confidence — insufficient detail | Pass | |
| 11 | Mixed English/Roman Urdu with a typo-heavy description | Estimate or fallback, English item names, no crash on parse | Pass | |
| 12 | Extremely long, rambling description covering 3 unrelated jobs at once | Low-confidence estimate or fallback — model shouldn't silently pick one job and ignore the rest | Fail | Model estimated only the first job mentioned without flagging the ambiguity — logged as a known limitation |

## Failure pattern found
Case 12: multi-job descriptions are silently narrowed to the first job mentioned instead of being flagged as ambiguous.

## Manual correction / improvement made
Added an explicit instruction to the system prompt: if the description covers more than one distinct job, set `needs_consultation: true` with a reason noting multiple jobs were detected, rather than estimating just one. Re-tested case 12 after the change — now correctly falls back.
