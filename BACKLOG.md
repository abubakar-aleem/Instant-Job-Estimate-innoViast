# Prioritized Backlog — Instant Job Estimate

Priority levels: **P0** (must-have, in current MVP) → **P3** (future/out of scope for Week 5).

## P0 — Core MVP (shipped)
- [x] Text input for job description (English or Roman Urdu)
- [x] Gemini 2.5 Flash Lite call, grounded in store context, returning structured JSON
- [x] Itemized estimate display with price range and confidence rating
- [x] Fallback to "needs in-store consultation" for vague/multi-job/out-of-scope input
- [x] Estimate clearly labeled as an estimate, not a final quote (disclaimer on result + footer)
- [x] API key handled session-only, in-memory, never stored or committed
- [x] Deployed live version (GitHub Pages)
- [x] README with problem, target user, validation evidence, setup, live link, roadmap
- [x] AI_USAGE.md, RISK_ETHICS.md, DATA_BOUNDARIES.md
- [x] Validation notes (3 observations: shopkeeper, customer, contractor)
- [x] Evaluation sheet (12 test cases, pass/fail, failure pattern documented)
- [x] Workflow diagram
- [x] Demo video

## P1 — Should-have (strengthens MVP quality)
- [x] Fallback message when request is too vague, mixed, or out of scope
- [x] Basic input validation (minimum description length before submit allowed)
- [x] Confirm no analytics/tracking scripts expose data (confirmed — only the Gemini API call leaves the browser; see `DATA_BOUNDARIES.md`)
- [ ] Wireframes finalized and added to repo
- [x] Demo video recorded

## P2 — Nice-to-have (if time allows)
- [x] Example prompts / quick-fill chips in the input field
- [x] Price shown as a range with confidence flag, not a single number (reduces false confidence)
- [x] Mobile-responsive layout
- [x] Loading/processing state after submit
- [ ] Session history persisting across page reloads (currently in-memory only, resets on refresh)

## P3 — Future (post-MVP, out of scope now)
- [ ] Real-time stock/pricing instead of static price bands
- [ ] Staff review dashboard before an estimate reaches the customer
- [ ] WhatsApp integration (customers already use this channel most)
- [ ] Broader language support beyond English/Roman Urdu
- [ ] Persistent estimate history across sessions

---
*Reflects the actual shipped repo state as of the Case 12 fix and full documentation package.*
