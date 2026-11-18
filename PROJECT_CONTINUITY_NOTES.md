# TriDashAI — Project Continuity Notes

Last updated: 14 November 2026

## GitHub repository
- Repository: https://github.com/kelvnwilson53-bot/Tradashai-test
- Working branch: `main`
- GitHub access was successfully tested from ChatGPT on 14 November 2026.

## Existing dashboard files verified
- `dashboard.html`
  - Retrieved successfully.
  - Blob SHA at time of check: `79b5fcbdcdef3e9a39afb322d560cfd3e4b994b2`
  - https://github.com/kelvnwilson53-bot/Tradashai-test/blob/main/dashboard.html
- `settings.html`
  - Retrieved successfully.
  - Blob SHA at time of check: `9ca85a5156dfafc8f215832a3449613db8d6b7e2`
  - https://github.com/kelvnwilson53-bot/Tradashai-test/blob/main/settings.html

Note: SHAs are snapshots from the date above; always fetch the latest files and SHAs before editing.

## Agreed working method
1. Continue from the existing repository and current code. Do not rebuild the dashboard from scratch.
2. Before editing, inspect the relevant dashboard/settings code and its Firebase connections.
3. Identify the requested changes and protect existing working functionality.
4. Make controlled, clearly described commits to the repository.
5. Test the changes and give the user straightforward instructions for checking them in the live dashboard.
6. Do not claim a change is live or tested unless that has actually been verified.

## Immediate next step
Resume the dashboard work. Ask which specific dashboard change the user wants tackled first if it has not already been specified in the active conversation.

## Separate business-planning note
The trial-acquisition forecast must model actual free-trial uptake from the initial 200 contacted prospects. Do not assume all 200 activate a trial. Track delivered emails, replies, expressions of interest, trial registrations/activations, usage, and paid conversions. Trial expenditure should be based on actual trial activations and actual usage; the previously discussed $6.30 per fully used trial is provisional, not a verified final cost.


## 18 November 2026 — Additional Information box and future arrival-time workflow

### Current task: finish the Advanced Setup layout
- The user wants to see and finalise the layout of the **Additional information** box in Advanced Setup before moving on.
- Keep this section simple: heading **Additional information**, a short explanation that it is optional and is for approximate journey times by service area plus customer arrival-update instructions, and one large free-text box.
- Suggested placeholder example: "For emergency call-outs, customers up to 10 miles away usually take 15–25 minutes; 10–20 miles can take 30–45 minutes, depending on traffic. These are estimates only. Check whether I am available or already on another job. If I confirm I am on my way and give an ETA, text the customer. Send another update when I confirm I am about 10 minutes away."
- Do not imply that the receptionist can promise attendance or an ETA from the guidance alone. This text is contractor guidance, not live confirmation.
- User is tired and has asked to pause the more involved development. Do not push the Google Maps / contractor confirmation work now.

### Saved for a later development stage: confirmed attendance and journey-time workflow
The user likes the idea but cannot work on it now. Preserve it for later:
1. Use the contractor's saved business location and the customer's full address to calculate an actual Google Maps driving route/time (not just a simple radius calculation). Use traffic-aware estimates where available. A service-area radius may help determine coverage, but does not reliably predict journey time.
2. Treat the route duration as an estimate only. The contractor must be contacted for each job and explicitly confirm whether they can attend.
3. Only after the contractor confirms attendance and confirms they are on the way / gives an expected departure time may TriDashAI calculate or communicate a customer-facing ETA. Never promise attendance or an arrival time based only on the saved availability status or map estimate.
4. Send the customer an SMS only after the contractor's confirmation and agreed ETA. Send a further update when the contractor confirms they are approximately 10 minutes away.
5. If nobody is available, the contractor declines, or the status is stale/unclear, be honest with the customer and do not invent an ETA.
6. Before implementation, inspect the existing Firebase/Twilio architecture and confirm the safe backend approach for Google Maps Routes/Directions API. Keep API credentials out of browser code. Check what customer and contractor contact details and notification mechanisms are already implemented; do not assume SMS dispatch/confirmation is wired up.
7. The current dashboard availability selector is only a manually saved status. It does not yet provide per-job contractor acceptance, departure confirmation, live map routing, or automatic customer ETA messages.


## 18 November 2026 — Practice customer (John Smith), dashboard data and testing continuity

### User's immediate concern
The user logs in through `tridashai.com`. The browser recognises the existing Firebase login and takes them straight past Quick Start to the activated dashboard. This is expected if the signed-in account's Firestore business profile has `quickStartComplete: true`. The user understands this as the John Smith practice customer journey and wants to see what a real customer would see, with the details they already entered. They are frustrated by repeatedly spending days correcting avoidable mistakes. Tomorrow's work must begin by inspecting the existing account/profile and current code, not by asking the user to repeat setup or rebuilding anything.

### What was verified in the current source on 18 November
- `dashboard.html` was fetched from `main`; blob SHA at inspection: `e1484325faae3e3716a604fb6262abc1ab6d8098`.
- Dashboard authentication uses Firebase Auth. After sign-in, it reads `businesses/{user.uid}` from Firestore.
- If the business document exists, it loads the fields in `quickFields`, including `businessName` and `businessPhone`, into the Quick Start form inputs.
- If `quickStartComplete` is true, the code hides Quick Start and shows the activated dashboard (`stage-2`). That explains why the user is taken straight past setup.
- The Quick Start submit handler saves the field `businessPhone` (along with the other Quick Start fields) to `businesses/{user.uid}`.
- The activated dashboard's current Call forwarding card is only a preview placeholder. It does not display the saved business number. Its forwarding button is disabled and says Preview.
- The AI receptionist switch is also explicitly a preview; it does not activate call answering or forwarding.
- Google Calendar is currently shown as not connected / preview. It is not a live connection.
- `settings.html` reads the same `businesses/{user.uid}` document and its displayed summary uses `savedProfile.businessPhone` for the phone field.

### Important: what has NOT yet been verified
- We have NOT inspected John's actual Firestore business document or confirmed the exact value stored in it.
- We have NOT established whether John's number is stored as `businessPhone`, `phone`, or another field. The earlier suggestion that there may be a `phone` versus `businessPhone` field mismatch is only a hypothesis until the actual practice profile is inspected. Do not present it as a confirmed cause.
- The earlier-mentioned number `+1 214-555-0147` has NOT been verified against the live Firestore profile. Do not treat it as authoritative, overwrite any value with it, or display it as John's confirmed number without checking the actual profile first.
- Source inspection does not prove that the live website is loading the same deployed revision or that Firebase security/rules and live data behave correctly. No end-to-end live customer test has yet been performed.

### Tomorrow's first task — diagnose, don't rebuild
1. Confirm which Firebase Auth account is signed in on the user's browser and that it is the intended John Smith practice account. Do not ask the user to sign out or create another account unless necessary.
2. Inspect the corresponding Firestore document at `businesses/{uid}` using an authorised, safe method. Do not expose credentials or ask the user to share passwords. Confirm the saved business name, business phone field(s), `quickStartComplete`, and other setup fields.
3. Compare the actual stored field names/values with the dashboard's `quickFields` and the settings page. Establish exactly where the existing business number went before changing data or code.
4. If the saved number exists, make the Call Forwarding card display that exact saved business number automatically. Do not require the customer to enter it a second time. Also show the separate TriDashAI receiving number only once one has actually been assigned.
5. If the saved number is missing or stored under a legacy field, preserve the original value and plan a safe compatibility/migration approach. Never overwrite or invent a number.
6. Keep the business number and the TriDashAI receiving number clearly distinguished. Explain that displaying them is separate from configuring carrier call forwarding.
7. Verify the change in the live signed-in practice account, including refresh/re-login behaviour if appropriate. Report separately what is source-verified and what is live-tested.

### Current customer journey / functionality status
- Firebase login and business-profile retrieval: implemented in source; user is reaching the activated dashboard.
- Quick Start data persistence and prefill: implemented in source; actual John Smith field values still need inspection.
- Quick Start bypass: expected when `quickStartComplete` is true.
- Business number shown in activated dashboard Call Forwarding card: not implemented yet.
- TriDashAI number assignment, carrier forwarding activation, live receptionist call answering, Google Calendar integration and live analytics: not connected/verified yet. Keep these limitations visible and do not imply that the dashboard preview controls are live.

### User's agreed approach
- Do not rebuild the dashboard or discard existing work.
- Preserve all existing business/profile data and functionality.
- Diagnose the practice account first, then fix the data display and test the customer journey in small, controlled steps.
- The user has paused work for the evening because they are tired. Resume tomorrow from this note and the actual source/profile inspection; do not ask them to repeat the whole story.
