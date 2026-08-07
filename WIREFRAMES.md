# Wireframes — Instant Job Estimate

Single-page flow matching the actual shipped MVP (`index.html`) — no login, no multi-page navigation, everything on one scrollable page.

## Screen 1 — Header + API Setup

```
┌─────────────────────────────────────────────┐
│ [Logo]  Akbar & Sons Sanitary Store  ● Online│
│         Describe your job — English or       │
│         Roman Urdu — get a material list     │
│         and price range.                     │
├───────────────────────────────────────────────┤
│  API Setup                                     │
│  [ Paste Gemini API key... ] [ Set Key ]       │
│  No key set yet — estimates won't run yet.     │
└───────────────────────────────────────────────┘
```

## Screen 2 — Describe the Job

```
┌───────────────────────────────────────────────┐
│  Describe the job                              │
│  e.g. "Bathroom mein commode aur wash basin    │
│  lagwana hai, purani pipeline bhi kharab hai"  │
│                                                 │
│  [Bathroom fitting] [Kitchen sink] [Water tank]│
│  [Pipe leak repair]                            │
│                                                 │
│  ┌───────────────────────────────────────────┐│
│  │ Type your job description here...          ││
│  └───────────────────────────────────────────┘│
│  Approx. area / property type (optional)       │
│  [__________________________]                  │
│                                                 │
│              [ Get Estimate ]                  │
└───────────────────────────────────────────────┘
```

## Screen 3 — Result (Estimate Returned)

```
┌───────────────────────────────────────────────┐
│  Your Estimate                                 │
│                                                 │
│  [Higher confidence]                           │
│  PKR 25,000 – 40,000                           │
│  ┌───────────┬─────┬───────────┬─────────────┐│
│  │ Item      │ Qty │ Price     │ Notes        ││
│  ├───────────┼─────┼───────────┼─────────────┤│
│  │ Commode   │ 1   │ 9k–18k    │ Polo brand   ││
│  │ Wash basin│ 1   │ 4k–10k    │ w/ fittings  ││
│  └───────────┴─────┴───────────┴─────────────┘│
│  Estimate only — confirm exact pricing, stock, │
│  and brand availability in-store.              │
└───────────────────────────────────────────────┘
```

## Screen 4 — Result (Fallback / Needs Consultation)

```
┌───────────────────────────────────────────────┐
│  Your Estimate                                 │
│                                                 │
│  ⚠ This job needs an in-store consultation.    │
│  Describes 3 separate jobs (bathroom, kitchen  │
│  leak, water tank) — each needs its own        │
│  estimate.                                     │
│                                                 │
│  Please visit or call the store so staff can   │
│  assess it properly.                           │
└───────────────────────────────────────────────┘
```

## Screen 5 — Past Estimates (Session History)

```
┌───────────────────────────────────────────────┐
│  Past Estimates (this session)                 │
│  ─────────────────────────────────────────────│
│  "Bathroom mein commode aur basin..."          │
│  PKR 25,000 – 40,000                           │
│  ─────────────────────────────────────────────│
│  "I need a whole new bathroom, kitchen..."     │
│  Flagged for in-store consultation             │
└───────────────────────────────────────────────┘
```

## Notes
- Matches the actual single-file MVP (`index.html`) exactly — no separate screens or navigation, all sections stack on one page
- Fallback screen (Screen 4) reflects the real fallback behavior after the Case 12 fix — see `AI_USAGE.md` and `evaluation.md`
- No login/account screens, since no persistent user data is stored — see `DATA_BOUNDARIES.md`
- Built directly in code rather than in Figma, given the single-file HTML approach used across the internship
