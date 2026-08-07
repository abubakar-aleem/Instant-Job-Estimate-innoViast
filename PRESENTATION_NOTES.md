# Presentation Notes — Instant Job Estimate (Week 5)

## 1. The Problem (30 sec)
Every estimate at Akbar & Sons — whether from a walk-in, phone call, or WhatsApp message — is prepared manually by the shopkeeper: checking each item, calculating prices, replying. This is slow, doesn't scale during busy hours, and gets slower still when the customer's request is vague, since it takes several rounds of follow-up to clarify.

Validated through direct observations with the shopkeeper, a regular customer, and a contractor/bulk buyer (see `validation-notes.md`) — all three independently pointed to the same bottleneck: manual checking + unclear requests = delay.

## 2. The Solution (30 sec)
A single-page AI estimator: customer describes their job in English or Roman Urdu, gets an itemized material list and PKR price range in seconds, with a confidence rating showing how much detail was given. If the request is too vague, mixes multiple unrelated jobs, or is outside plumbing/sanitary scope, it automatically routes to "needs in-store consultation" instead of guessing — keeping the shopkeeper as the final authority on real pricing and stock.

## 3. How It Works (45 sec)
- Customer types a job description → sent to Gemini 2.5 Flash Lite with a system prompt grounded in the store's actual brands, categories, and price bands
- Model returns structured JSON: either an itemized estimate or a fallback reason
- Every estimate carries a disclaimer — it's a planning reference, not a final quote
- Full flow diagrammed in `workflow-diagram.md`: input → scope/detail check → model call → structured output → human review layer

## 4. Testing & a Real Fix (45 sec)
Ran 12 test cases spanning clear requests, Roman Urdu, vague input, out-of-scope requests, and edge cases (empty input, rambling multi-job descriptions).

Found a real failure: a long, detailed description covering 3 unrelated jobs (bathroom, kitchen leak, water tank) got silently estimated as if it were one job — the model treated "detailed" as "unambiguous," which isn't true when the detail spans multiple jobs.

**Fix:** rewrote the ambiguity rule in the prompt to state explicitly that length/detail doesn't resolve ambiguity, named this exact failure mode, and added a worked multi-job example. Retested — now correctly falls back to consultation, naming each job found.

This is the part worth walking a mentor through in detail — it shows the evaluation loop actually caught something and the fix was targeted at the root cause, not a band-aid.

## 5. Responsible AI Design (30 sec)
- No customer PII sent to the model — just the free-text job description
- API key lives only in browser memory for the session, never stored or committed
- Price ranges are explicitly illustrative, not live stock data — disclaimer on every result
- Out-of-scope work (electrical, structural) is never guessed at, always deferred to staff
- Full risk/ethics breakdown in `RISK_ETHICS.md` and `DATA_BOUNDARIES.md`

## 6. What's Next (15 sec)
- Real-time stock/pricing instead of static price bands
- Staff review dashboard before estimates reach customers
- WhatsApp integration, since that's already the channel customers use most
- Broader language coverage beyond English/Roman Urdu

## Anticipated Questions
- **"What if the AI gives a wrong price?"** → Every estimate carries a disclaimer, confidence rating, and is explicitly a reference — final pricing is always confirmed in-store by staff.
- **"Why not just always show an estimate?"** → Because a wrong estimate on an ambiguous or multi-job request is worse than no estimate — the fallback protects both the customer and the store from a bad guess.
- **"Is the API key safe?"** → Yes — session-only, in-memory, never persisted or committed; verified nothing is exposed in the repo.
