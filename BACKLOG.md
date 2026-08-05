# Prioritized Backlog — Instant Job Estimate

Priority levels: **P0** (must-have, in current MVP or blocking submission) → 
**P3** (future/nice-to-have, out of scope for Week 5).

## P0 — Core MVP (required for submission)
- [x] Text input field for job description
- [x] Rule-based logic to map description → estimate
- [x] Display estimate result to user
- [x] Label result clearly as "estimate, not final quote"
- [x] Deploy live version (GitHub Pages / hosting)
- [x] README with problem, target user, setup, live link
- [x] AI_USAGE.md, RISK_ETHICS.md, DATA_BOUNDARIES.md
- [x] Validation notes (3+ user interviews/observations)
- [x] Evaluation sheet (10+ test cases, pass/fail)

## P1 — Should-have (strengthens MVP quality)
- [ ] Fallback message when input doesn't match any rule confidently 
      (e.g. "Not enough detail — try adding job type and size")
- [ ] Basic input validation (empty input, extremely short input)
- [ ] Confirm no analytics/tracking scripts expose data (per DATA_BOUNDARIES.md)
- [ ] Wireframes finalized and added to repo
- [ ] Demo video recorded and linked in README

## P2 — Nice-to-have (if time allows)
- [ ] Example prompts / placeholder text in the input field to guide users
- [ ] Simple price range instead of single number (reduces false confidence)
- [ ] Mobile-responsive layout polish
- [ ] Basic loading/processing state after submit

## P3 — Future (post-MVP, out of scope now)
- [ ] Replace rule-based logic with real AI model (LLM or trained classifier)
- [ ] Add photo upload as additional input
- [ ] User accounts / saved estimate history
- [ ] Human-in-the-loop review before showing final estimate
- [ ] Multi-language support

---
*Note: adjust checked/unchecked items above to match actual current repo state 
before submitting — this backlog assumes the P0 items match what's already built.*
