# Project Post Draft — Instant Job Estimate

*Concise post for showcase (LinkedIn / portfolio / demo submission). 
Target length: short, scannable, no jargon.*

---

**🔧 Built: Instant Job Estimate**

Ever needed a quick sense of what a repair job might cost — before calling 
anyone? I built a simple tool that gives users an instant cost estimate just 
from describing their job in plain text.

**The problem:** People often don't know if a job is a $50 fix or a $500 one 
until a contractor shows up. That gap causes hesitation and wasted time on 
both sides.

**What I built:** A lightweight, client-side MVP where a user types a short 
job description (e.g. "leaking kitchen faucet") and gets back an instant 
estimate — no signup, no data collection, nothing leaves the browser.

**How it works:** Right now it runs on rule-based logic that matches job 
descriptions to pricing patterns. I chose to be upfront about this rather 
than oversell it as "AI-powered" — it's a transparent MVP, not a black box.

**What I validated:** I talked to 3 people involved in the real process — a 
shopkeeper, a regular customer, and a contractor — at a plumbing/sanitary 
store. All three pointed to the same bottleneck: incomplete or unclear 
requests force multiple rounds of back-and-forth before any estimate can be 
given. That directly shaped the tool's fallback behavior — when input is too 
vague, it asks for more detail instead of guessing, rather than returning a 
confident-looking number for an unclear request.

**What's next:** Swapping the rule engine for a real model to handle more 
varied phrasing, and adding a confidence-based fallback so the tool says 
"I'm not sure" instead of guessing on unclear input.

🔗 Live demo: https://abubakar-aleem.github.io/Instant-Job-Estimate-innoViast/
💻 Code: https://github.com/abubakar-aleem/Instant-Job-Estimate-innoViast

---

*Post is now fully filled in with your real validation data. Keep total post 
under ~150 words if posting to LinkedIn — trim the "What I validated" 
paragraph if needed.*
