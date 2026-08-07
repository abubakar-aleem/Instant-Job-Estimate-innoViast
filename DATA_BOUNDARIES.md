# Data Boundary Notes — Instant Job Estimate

## 1. What Data Is Collected
- Free-text job description entered by the customer
- Optional property/context notes (e.g. "1 bathroom, small house")
- Nothing else — no name, phone number, address, or account info is requested anywhere in the app

## 2. What Data Leaves the Device
- The job description and optional property notes **are sent to Google's Gemini API** (`generativelanguage.googleapis.com`) to generate the estimate — this is a real network call, not a client-only simulation
- No personally identifiable information (PII) is included in that request — only the free-text job details
- Nothing else leaves the device: no analytics, no tracking scripts, no third-party calls other than the Gemini API itself

## 3. What Is NOT Collected
- No PII: name, email, phone, address
- No photos or images
- No location/GPS data
- No account creation or login — the tool is used anonymously, per session

## 4. API Key Handling
- The Gemini API key is entered by the user into the app for their own session
- Held only in a JavaScript variable in browser memory — never written to localStorage, cookies, or the repository
- The input field is cleared immediately after the key is set, so the raw key isn't left visible in the DOM
- A short SHA-256 fingerprint (first 8 hex characters) is shown to the user to confirm which key is active, without displaying the key itself

## 5. Data Retention
- Nothing is persisted server-side — there is no backend server for this app
- Session history (past estimates shown in the "Past Estimates" panel) exists only in browser memory and is lost on page refresh or close
- Google's own data handling for API requests is governed by Google's Gemini API terms, outside this project's control — no additional data is sent beyond what's needed to generate the estimate

## 6. Why This Boundary Was Chosen
- Sending only the job description (no PII) to the model keeps the assignment's "no exposed credentials or sensitive user data" requirement satisfied while still using a real AI model, not a rule-based simulation
- Session-only API key handling avoids any credential ever being committed to the repo or stored beyond the browser tab's lifetime

## 7. Future Considerations
- If a backend is added (see `README.md` roadmap) to support staff review or persistent history, this document must be updated to disclose server-side storage, retention period, and access control
- If contact info is ever collected (e.g. to send the estimate to the customer directly), this file must be updated with storage method and consent handling
