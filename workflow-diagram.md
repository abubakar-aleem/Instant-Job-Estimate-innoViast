# AI Workflow Diagram — Instant Job Estimate

```mermaid
flowchart TD
    A[Customer types job description<br/>English or Roman Urdu] --> B{Enough detail<br/>and in scope?}
    B -- No / unclear / out of scope --> F[Fallback:<br/>'Needs in-store consultation'<br/>+ reason shown to customer]
    B -- Yes --> C[Gemini 2.5 Flash Lite<br/>System prompt + store price-band context<br/>+ customer's description]
    C --> D[Structured JSON output:<br/>item list, qty, price range,<br/>total range, confidence flag]
    D --> E[Rendered estimate shown to customer<br/>with mandatory disclaimer]
    E --> G[Human review layer:<br/>customer/staff confirm exact<br/>pricing & stock in-store before purchase]
    F --> G
```

## Notes
- The branch at B is enforced inside the model's own instructions (the prompt requires it to self-assess before answering), not by separate application logic — this is documented as a limitation: a second, independent check would strengthen it.
- Every path — confident estimate or fallback — ends at the same human checkpoint (G). No output is ever treated as final pricing.
- The confidence flag (`high`/`low`) attached to every non-fallback estimate is a second, lighter-weight signal to the customer on top of the binary fallback gate.
