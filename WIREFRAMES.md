# Wireframes — Instant Job Estimate

Simple single-page flow, matching the current client-side MVP (no login, 
no multi-page navigation).

## Screen 1 — Landing / Input

```
┌─────────────────────────────────────────┐
│  [Logo]        Instant Job Estimate      │
├─────────────────────────────────────────┤
│                                           │
│   Get an instant estimate for your job   │
│                                           │
│   ┌───────────────────────────────────┐ │
│   │ Describe the job                   │ │
│   │ e.g. "Fix a leaking kitchen        │ │
│   │ faucet"                            │ │
│   │                                     │ │
│   └───────────────────────────────────┘ │
│                                           │
│              [ Get Estimate ]            │
│                                           │
│   ⚠ This is an estimate, not a final     │
│     quote.                               │
│                                           │
└─────────────────────────────────────────┘
```

## Screen 2 — Result (Match Found)

```
┌─────────────────────────────────────────┐
│  [Logo]        Instant Job Estimate      │
├─────────────────────────────────────────┤
│                                           │
│   Your Estimate                          │
│                                           │
│   ┌───────────────────────────────────┐ │
│   │  Job type: Plumbing – Faucet Repair│ │
│   │  Estimated cost: $80 – $150        │ │
│   └───────────────────────────────────┘ │
│                                           │
│   ⚠ Estimate only. Actual cost may vary  │
│     based on site conditions.            │
│                                           │
│              [ Try Another ]             │
│                                           │
└─────────────────────────────────────────┘
```

## Screen 3 — Result (No Confident Match / Fallback)

```
┌─────────────────────────────────────────┐
│  [Logo]        Instant Job Estimate      │
├─────────────────────────────────────────┤
│                                           │
│   We couldn't confidently estimate this  │
│   job.                                   │
│                                           │
│   Try adding more detail:                │
│   • What type of job is it?              │
│   • Roughly what size/scope?             │
│                                           │
│              [ Try Again ]               │
│                                           │
└─────────────────────────────────────────┘
```

## Notes
- Single-page, no navigation menu — matches the actual MVP scope (index.html only).
- Fallback screen (Screen 3) reflects the fallback behavior documented in 
  RISK_ETHICS.md — update this wireframe if actual fallback UI differs.
- No login/account screens, since no user data is stored (per DATA_BOUNDARIES.md).

*These are text-based wireframes matching the MVP's actual scope. Replace with 
Figma screenshots if you created higher-fidelity mockups — cite the tool used 
in README if so (Figma was listed as a suggested tool).*
