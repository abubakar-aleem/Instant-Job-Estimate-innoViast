# Project Post Draft — Instant Job Estimate

*Concise post for showcase (LinkedIn / portfolio / demo submission).*

---

**🔧 Built: Instant Job Estimate — for Akbar & Sons Sanitary Store**

Ever needed a rough price before deciding whether to even start a job? I built an AI-powered tool for my family's plumbing/sanitary store that gives customers an instant estimate — just from describing the job in plain English or Roman Urdu.

**The problem:** Every estimate at the store currently goes through the shopkeeper manually — checking items, calculating prices, replying over WhatsApp, call, or in person. I validated this with the shopkeeper, a regular customer, and a contractor: all three pointed to the same bottleneck — manual checking plus unclear requests means slow turnaround, especially during busy hours.

**What I built:** A single-page tool powered by Google's Gemini 2.5 Flash Lite. A customer describes their job — "Bathroom mein commode aur basin lagwana hai" or "installing a water tank on the roof" — and gets back an itemized material list with a PKR price range and a confidence rating, grounded in the store's actual brands and product categories.

**Built responsibly:** When a request is too vague, mixes multiple unrelated jobs, or falls outside plumbing/sanitary work, the tool doesn't guess — it flags "needs in-store consultation" and explains why, keeping the shopkeeper as the final authority on real pricing and stock. No customer data is collected, and the API key never leaves the browser session.

**Caught a real bug during testing:** One of my 12 test cases — a long, rambling description covering 3 unrelated jobs — got silently estimated as if it were one job. Fixed by tightening the prompt to explicitly treat "detailed" and "unambiguous" as different things, then retested and confirmed the fix.

🔗 Live demo: https://abubakar-aleem.github.io/Instant-Job-Estimate-innoViast/
💻 Code: https://github.com/abubakar-aleem/Instant-Job-Estimate-innoViast

---
*~160 words — trim the "Caught a real bug" paragraph if posting somewhere with a strict length limit.*
