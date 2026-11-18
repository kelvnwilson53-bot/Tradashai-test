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
