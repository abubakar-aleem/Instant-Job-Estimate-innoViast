# Data Boundary Notes — Instant Job Estimate

## 1. What Data Is Collected
- Free-text job description entered by the user.
- No name, contact info, photos, or location is collected.

## 2. What Happens to the Data
- All processing happens **client-side**, in the user's browser.
- No data is sent to a backend server, database, or third-party API.
- Nothing is persisted — once the page is closed or refreshed, the input is gone.

## 3. What Is NOT Collected
- No personally identifiable information (PII): name, email, phone, address.
- No photos or images.
- No location/GPS data.
- No account creation or login — the tool is used anonymously.

## 4. Third-Party Exposure
- No AI API (e.g. OpenAI) is called, so no user input leaves the device.
- No analytics/tracking scripts currently send data externally. 
  [Confirm this is true — check index.html for any embedded scripts like 
  Google Analytics before submitting.]

## 5. Why This Boundary Was Chosen
- Keeping everything client-side avoids handling sensitive user data entirely 
  for this MVP stage, removing the need for consent flows, storage security, 
  or a privacy policy at this point.
- This matches the assignment's requirement to never expose credentials or 
  sensitive user data — there is no sensitive data to expose in this version.

## 6. Future Considerations
- If the product moves to a real AI model via an API, the job description 
  would leave the client and this document must be updated to disclose that, 
  along with what the API provider does with submitted data.
- If contact info is ever collected (e.g. to send the estimate), this file 
  must be updated with storage method, retention, and access control.
