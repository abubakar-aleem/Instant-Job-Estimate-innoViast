# Instant Job Estimate — Akbar & Sons Sanitary Store

An AI-assisted first-pass estimator for plumbing and sanitary jobs. A customer describes their job in English or Roman Urdu and gets an approximate material list and PKR price range in seconds — with an automatic handoff to in-store staff whenever the request is too vague, mixes multiple jobs, or falls outside plumbing/sanitary work.

Built as Week 5 of the InnoViast AI Chatbot Developer Internship (Human-Centered AI Product Innovation Sprint).

---

## Problem
Customers and contractors currently get every plumbing/sanitary estimate the same way — visit the shop, call, or send requirements over WhatsApp — and the shopkeeper manually checks each item and price before replying. This is slow, doesn't scale during busy hours, and gets even slower when the customer's own request is unclear, since it takes several follow-up messages to clarify. See `validation-notes.md` for the full observations this is based on.

## Target User
Regular customers and contractors/bulk buyers of Akbar & Sons who want a fast reference price range before deciding how to proceed — without waiting on manual back-and-forth for every request.

## Validation Evidence
Grounded in observations from the shopkeeper, a regular customer, and a contractor/bulk buyer — full write-up, persona, and problem statement in [`validation-notes.md`](./validation-notes.md).

## Features
- Describe a job in **English or Roman Urdu**, get an itemized estimate with a PKR price range
- **Confidence rating** (high/low) based on how much detail was given
- **Automatic fallback** to "needs in-store consultation" for vague, contradictory, multi-job, or out-of-scope (e.g. electrical/structural) requests
- Quick-fill example chips for common job types (bathroom, kitchen, water tank, leak repair)
- Session history of past estimates
- API key entered per-session only — never stored or committed

## Tech Stack
- Single-file HTML/CSS/JavaScript (no build step, no backend)
- Google **Gemini 2.5 Flash Lite** via direct browser fetch to `generateContent`
- Fonts: Cinzel (headings) + Raleway (body), matching the Akbar & Sons brand used across earlier internship weeks

## Setup
1. Clone or download this repo
2. Make sure `logo.png` is in the same folder as `index.html`
3. Open `index.html` in a browser (or serve via GitHub Pages)
4. Get a free Gemini API key from [Google AI Studio](https://aistudio.google.com/)
5. Paste the key into the "API Setup" card in the app — it's used only for your browser session and never leaves your device or gets stored

## Screenshots
See `1.png`–`6.png` in this repo for interface screenshots covering the main flow, an estimate result, and a fallback case.

## Live Link
`<https://abubakar-aleem.github.io/Instant-Job-Estimate-innoViast/>`

## Evaluation
10+ test cases covering clear requests, Roman Urdu input, vague input, multi-job input, and out-of-scope requests — including one failure found and fixed during testing. Full results in [`evaluation.md`](./evaluation.md).

## AI Usage, Risks & Limitations
Prompt log, model details, known limitations, the Case 12 fix, and risk/ethics + data boundary notes are documented in [`AI_USAGE.md`](./AI_USAGE.md).

## Workflow Diagram
See [`workflow-diagram.md`](./workflow-diagram.md) for the input → model → output → human review/fallback flow.

## Roadmap
- Add a lightweight backend to store real-time stock/pricing instead of static price bands
- Let staff review and confirm AI estimates from a simple dashboard before they're sent to the customer
- Expand language coverage beyond English/Roman Urdu
- Add WhatsApp integration so customers can get estimates in the channel they already use most

---
Akbar & Sons Sanitary Store · Main Defence Ghazi Road, near Jamia Masjid Sadiqia, Lahore · 9 AM–9 PM
