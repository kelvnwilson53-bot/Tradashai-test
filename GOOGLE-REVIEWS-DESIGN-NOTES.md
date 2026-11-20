# Google Reviews — Dashboard Design & Delivery Notes

## Purpose

Explain the Google review service clearly during the contractor's 7-day TriDashAI trial. The dashboard should show what the service is intended to deliver without presenting sample values as live results or implying integrations are already operational.

## Contractor experience

### 1. Review requests after completed jobs
- A job must be marked complete by the contractor or reported complete by a supported job-management integration.
- TriDashAI sends a polite SMS containing the contractor's Google review link after a configurable delay (initial proposal: about two hours).
- Record the job reference, customer contact, request time, message status and provider delivery result where available.
- A request sent or SMS delivered is not proof that a review was submitted.
- Invite customers consistently to leave an honest review. Do not filter invitations by expected satisfaction, discourage negative feedback, or offer incentives for positive reviews.

### 2. Google profile health
After the contractor authorises access to a verified Google Business Profile, show data returned by Google's Business Profile API:
- Current average star rating.
- Total review count.
- New reviews in the selected period.
- Rating and review-count trend over time.
- Review-response coverage and outstanding reviews.

Label the source and last successful sync time. Do not invent or estimate live values. Show an unavailable state if the connection or sync is not working.

### 3. Sarah's review replies
- Detect new reviews through Google Business Profile notifications where supported.
- Retrieve the review and check whether a reply already exists.
- Sarah drafts a response based on the actual review and contractor's business context.
- Contractor approves or edits the draft before publication at launch.
- Flag low ratings, complaints, safety allegations, legal/insurance issues, personal information and other sensitive matters for human review.
- Submit the approved reply through Google's API and track its moderation/publication status. Do not claim a reply is public until confirmed.
- Use notifications for prompt processing plus a scheduled daily reconciliation check to catch missed events. This cadence is a proposed product design, not an existing service.

## Dashboard layout

The Google Reviews panel is placed within the activated dashboard and linked from the hamburger navigation. It contains:
1. Google Business Profile health: rating, total reviews, new reviews and replies published.
2. Review requests: requests sent and SMS delivery results.
3. Sarah's replies: drafts awaiting approval and response status.
4. An expandable “How the service works” explanation for trial users.

The current panel is a design/preview only. Dashes indicate that live values are not connected. The sample Sarah reply is explicitly labelled as an example.

## Implementation dependencies — not yet complete

1. Google OAuth consent and secure account/location selection for each contractor.
2. Verify the contractor's Business Profile is eligible and authorised.
3. Store the Google review link and profile/location identifiers per business.
4. Define a job-completion trigger. The current dashboard does not yet provide a complete job-management workflow.
5. Connect Twilio SMS sending, delivery callbacks and request audit records.
6. Implement Google Business Profile API review retrieval and response posting.
7. Configure Google notifications (Pub/Sub) and a daily reconciliation job.
8. Store review records, drafts, approvals, published-response status and sync timestamps in Firebase.
9. Enforce per-business data isolation, secure token storage, retry handling, duplicate-event protection and audit logging.
10. Test with a real authorised test profile before enabling the feature for paying customers.

## Important product boundaries

- Google review data and publishing depend on Google authorisation, API access and a verified eligible Business Profile.
- Google may moderate submitted replies; submission is not proof of immediate public display.
- SMS delivery status does not prove that a review was left.
- Sarah must never invent review content or reply to a review she has not retrieved.
- At launch, replies require contractor approval. Automatic publishing may be considered later as an explicit opt-in after safety and quality testing.
- The dashboard preview must not be described as a live, connected service until the complete end-to-end workflow has been implemented and verified.
