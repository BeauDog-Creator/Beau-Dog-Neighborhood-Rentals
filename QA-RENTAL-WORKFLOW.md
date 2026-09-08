# Beau Dog Neighbor Rentals — Rental Workflow QA

## Goal
Make every rental follow a clear, auditable lifecycle from the first request through completion or cancellation.

## Required lifecycle
1. Pending owner approval
2. Accepted / Declined
3. Confirmed
4. Ready for pickup
5. Active rental
6. Return pending
7. Completed
8. Cancelled / Disputed

## Current prototype findings

### Working now
- Renter can open a listing and send a rental request.
- Start date and number of days are captured.
- Rental is saved to the local `rentals` data store.
- The new rental initially shows `Pending owner approval`.
- Owner name is stored with the request.
- Payment disclaimer is shown: renter and owner arrange payment directly.
- Safety guidance appears in the rental area.
- A renter can cancel a saved request.

### Launch blockers / defects

#### 1. No owner Accept / Decline action
The prototype creates a pending request but there is no owner-side control to accept or decline it.

**Fix:** Add owner actions for Accept and Decline, with status history.

#### 2. No confirmed state
A request cannot advance from accepted to a clearly confirmed rental.

**Fix:** Add a `Confirmed` stage after both sides acknowledge the rental terms/payment arrangement.

#### 3. Cancellation currently deletes the rental record
The current Cancel button removes the rental from local storage entirely.

**Fix:** Preserve the record and change status to `Cancelled`, including date/time and who cancelled.

#### 4. Request message is not saved
The request form includes a message field, but the submitted rental object does not currently store that message.

**Fix:** Save the renter message with the rental request and show it in the rental detail view.

#### 5. No agreed price/deposit/payment record
The app tells renter and owner to arrange payment directly, but there is no place to record what they agreed to.

**Fix:** Add fields for:
- agreed rental price
- security deposit
- payment method
- payment timing
- both-side agreement confirmation

#### 6. Exact address release is not actually tied to approval
The UI says the address stays private until confirmation, but the prototype has no real state-based address release logic.

**Fix:** Never expose exact pickup details before `Confirmed`. In production this must be enforced by the backend, not only by UI.

#### 7. No pickup handoff state
There is no Ready for Pickup / Picked Up transition.

**Fix:** Add owner `Ready for Pickup` and renter `Picked Up` controls, later paired with a PIN or handoff confirmation.

#### 8. No active-rental state
The app cannot show that equipment is currently out on rent.

**Fix:** Add `Active rental`, expected return date, and overdue detection.

#### 9. No return workflow
There is no Returned / Return Accepted step.

**Fix:** Add `Return Pending`, owner inspection, and `Completed` state.

#### 10. No condition-photo connection
Safety guidance says to take photos, but photos are not attached to the rental record.

**Fix:** Add pickup and return condition-photo sets when storage/backend is available.

#### 11. No dispute path tied to a rental
The general reporting system exists, but a dispute is not yet attached to a specific rental lifecycle.

**Fix:** Add `Disputed` status and link reports, photos, messages, and timeline to the rental ID.

## Recommended prototype implementation order
1. Preserve existing rental records and replace destructive Cancel with `Cancelled` status.
2. Save request message, requested dates, price, and owner/renter identifiers.
3. Add status timeline to each rental.
4. Add prototype Accept / Decline controls.
5. Add Confirmed → Ready for Pickup → Active → Return Pending → Completed controls.
6. Add agreed payment/deposit fields.
7. Add pickup/return PIN and condition photos after the core state machine is stable.

## Production note
The current prototype uses browser `localStorage`, so renter-side and owner-side state is not actually shared across devices. The workflow can be prototyped locally, but true owner approval, cross-device messaging, privacy enforcement, notifications, and status synchronization require the production backend/accounts system.
