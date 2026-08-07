# AI_USAGE.md — Instant Job Estimate

## Model Used
Google **Gemini 2.5 Flash Lite**, called directly from the browser via `generateContent`, using a `systemInstruction` (system prompt) + the customer's job description as the user message. Temperature set to 0.3 to keep output consistent and reduce creative drift on pricing.

## Why This Model / Approach
- Fast, low-cost model suited to a short structured-output task (single JSON response per request).
- No backend server — API key is entered by the user for their own session only, matching the single-HTML-file pattern used across the internship's earlier weeks.

## Prompt Structure (Prompt Log)

**System prompt** (fixed, defined once in code) includes, in order:
1. Role framing — "estimating assistant for Akbar & Sons Sanitary Store"
2. `STORE_CONTEXT` — condensed store knowledge base: brands carried, product categories, and illustrative PKR price bands per common job type
3. Output rules:
   - Respond with valid JSON only, no markdown fences
   - Trigger `needs_consultation: true` for vague, contradictory, multi-job, or out-of-scope requests — with an explicit note that length/detail does not resolve ambiguity (added after evaluation testing, see below)
   - Otherwise return itemized `items`, `total_range`, and a `confidence` rating
   - Always include a fixed disclaimer string
4. A worked example showing a multi-job input mapped to `needs_consultation: true`
5. The exact JSON shape expected

**User message per request:**
```
Job description: <customer's text>
Property/context notes: <optional context or "none given">
```

### Sample runs (from evaluation.md testing)

| Input | Output behavior |
|---|---|
| "New commode and wash basin for one bathroom" | Itemized estimate, high confidence |
| "Bathroom mein commode aur basin lagwana hai" (Roman Urdu, same job) | Itemized estimate, high confidence, English item names |
| "Something's wrong with my pipes" | Fallback — too vague |
| "Rewire my kitchen's electrical outlets" | Fallback — out of scope (not plumbing) |
| Long rambling description covering 3 unrelated jobs | **Initially failed** — model silently estimated only one job. Fixed by strengthening rule 2 with an explicit "detail ≠ singularity" instruction and a worked multi-job example (see Known Limitations & Fixes below) |

## Known Limitations
- **Price ranges are illustrative, not live stock/pricing** — the model works from a condensed price band table hard-coded into the prompt, not real-time inventory or pricing. This is why every estimate carries a mandatory disclaimer and final pricing is always confirmed in-store.
- **Ambiguity handling depends entirely on prompt instructions**, not a deterministic rule — a sufficiently unusual phrasing could still slip past the `needs_consultation` trigger. The fallback is a safety net, not a guarantee.
- **No conversation memory** — each request is stateless; the model can't ask a clarifying follow-up question, it can only accept or flag-for-consultation in one pass.
- **Language coverage** — tuned for English and Roman Urdu; other languages or heavy code-mixing haven't been tested.

## Fix Applied (from Evaluation — Case 12)
**Problem found:** A long, detailed description covering 3 unrelated jobs (bathroom, kitchen leak, water tank) was answered as a single estimate instead of triggering the multi-job fallback — the model treated "detailed" as "unambiguous," which isn't true when the detail spans multiple separate jobs.

**Fix:** Rewrote rule 2 in the system prompt to explicitly state that length/detail does not resolve ambiguity, named "silently estimating only one of several described jobs" as a critical failure (not an acceptable simplification), and added a worked multi-job example for the model to pattern-match against.

**Result:** Re-tested after the fix — multi-job descriptions now correctly return `needs_consultation: true` with a reason naming each job found.

## Risk / Ethics Analysis
- **Risk — incorrect estimate causes customer confusion or a bad purchasing decision.** Mitigated by: (1) mandatory disclaimer on every estimate, (2) `confidence` flag so low-detail requests are visibly less certain, (3) fallback to human staff for anything ambiguous, multi-job, or out of scope.
- **Risk — AI treated as authoritative pricing.** Mitigated by explicit UI/footer language: "This is an AI-generated estimate for planning purposes only. Final pricing is confirmed in-store."
- **Out of scope by design:** electrical, structural, or non-plumbing work is explicitly routed to `needs_consultation` rather than guessed at.
- **Human review layer:** every estimate — whether a price range or a fallback message — is a starting point for a real conversation with store staff, not a final transaction.

## Data Boundary Notes
- No customer personal data (name, phone number, address) is collected or sent to the model — only the free-text job description and an optional property-type note.
- The Gemini API key is entered by the user each session, held only in a JavaScript variable in memory, and cleared from the input field immediately after being set. It is never written to localStorage, a cookie, or the repository.
- No conversation history or customer data is persisted server-side — there is no server; everything runs client-side in the browser for the duration of the session.
