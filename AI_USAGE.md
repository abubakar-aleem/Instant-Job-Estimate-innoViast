# AI_USAGE.md — Instant Job Estimate

## Model
Google **Gemini 2.5 Flash Lite**, called client-side via the `generateContent` REST endpoint (`x-goog-api-key` header). Temperature set to `0.3` to keep outputs consistent and reduce creative drift in pricing.

## What the AI is used for
The model takes a customer's free-text job description (English or Roman Urdu) plus a fixed store-context block (brands, categories, illustrative PKR price bands) and returns a structured JSON estimate: item list, quantities, price ranges, a total range, and a confidence flag. If the request is too vague, mixes multiple unrelated jobs, or falls outside plumbing/sanitary work, the model returns a fallback flag instead of guessing.

## Prompt structure
The system prompt has five fixed parts:
1. **Role framing** — "estimating assistant for Akbar & Sons Sanitary Store"
2. **Store context** — brands, categories, and illustrative price bands (hard-coded, not fetched live)
3. **Rules** — strict JSON-only output, when to trigger the consultation fallback, English item naming, mandatory disclaimer
4. **A worked example** — one multi-job input mapped to the expected fallback output, added specifically to fix a failure found during testing (see below)
5. **Output JSON shape** — exact keys the frontend expects, so rendering never breaks on missing fields

The user message passed alongside it is just the raw job description plus an optional property/context note.

## Prompt log (representative)
| Input | Output (summarized) |
|---|---|
| "New commode and wash basin for one bathroom" | Estimate, high confidence |
| "Bathroom mein commode aur basin lagwana hai" (Roman Urdu) | Estimate, high confidence, English item names |
| "Something's wrong with my pipes" | Fallback — too vague |
| "Rewire my kitchen's electrical outlets" | Fallback — out of scope |
| "I need a new bathroom, my kitchen sink is also leaking, and I want a water tank installed too" | Fallback — multiple unrelated jobs named individually |

Full 12-case log with pass/fail results lives in `evaluation.md`.

## Known limitations
- **Price ranges are illustrative, not live stock data.** They're hard-coded in the prompt and won't reflect real-time price or stock changes — every estimate carries a disclaimer directing the customer to confirm in-store.
- **No live inventory check.** The model can suggest an item that's temporarily out of stock.
- **Ambiguity handling is prompt-based, not rule-based.** Edge cases (extremely long/rambling multi-job descriptions) initially slipped past the fallback logic — see Risk & Fix below. Prompt-only safeguards can still be imperfect on inputs not resembling anything in testing.
- **Roman Urdu understanding depends on the model's own language handling** — not a custom NLP pipeline — so unusual spellings or heavy code-mixing could reduce accuracy.
- **Single-turn only.** The tool doesn't ask clarifying follow-up questions; it either estimates or hands off to in-store staff.

## Risk & Fix — multi-job silent estimation
**Risk found during evaluation (test case 12):** a long, rambling description covering 3 unrelated jobs was answered as if it were a single job, silently ignoring two of the three — the opposite of the intended fallback behavior, and the kind of error that could give a customer a materially wrong (too-low) price.

**Fix applied:** the system prompt was rewritten to state explicitly that length/detail does not resolve ambiguity, name "silently picking one job from several" as a named failure mode, and include a worked multi-job example showing the expected fallback response. This is a prompt-level mitigation; it was re-tested against the same case afterward (see `evaluation.md`).

## Risk & ethics summary
- **Harm if wrong:** an incorrect estimate could mislead a customer's budget expectations. Mitigated by (a) the mandatory disclaimer on every estimate, (b) the confidence flag distinguishing well-specified vs. vague requests, and (c) the human-review fallback for anything ambiguous or out of scope.
- **Scope boundaries:** the model is explicitly told to defer anything outside plumbing/sanitary work (electrical, structural) rather than attempt an estimate it has no real basis for.
- **Final authority stays human.** Every estimate — fallback or not — ends with the same instruction: confirm exact pricing, stock, and brand availability in-store. The AI is a first-pass filter, not a replacement for the shopkeeper.

## Data boundaries
- No customer personal data (name, phone number, address) is collected or sent to the model — only the job description text and an optional property-type note.
- The Gemini API key is entered per-session, held in a JS variable in memory, and never written to localStorage, cookies, or the repository. The input field is cleared immediately after the key is set.
- No conversation history or estimate data is persisted server-side; the session history list exists only in-browser and clears on refresh.
