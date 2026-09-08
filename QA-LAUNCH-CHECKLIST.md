# Beau Dog Neighbor Rentals — Launch QA Checklist

## Free vs Plus pricing flow

Status checked: September 8, 2026

### Free plan
- [x] New profiles start on the Free plan.
- [x] Free users can browse equipment.
- [x] Free users can request rentals.
- [x] Free users can use Map View.
- [x] Free users can use Favorites and Safety tools.
- [x] Free users can create listing #1.
- [x] Free users can create listing #2.
- [x] Attempting to create listing #3 is blocked and opens Plans & Pricing.
- [x] Existing listings remain editable on the Free plan.
- [x] Existing listings can be removed on the Free plan.

### Beau Dog Plus
- [x] Monthly prototype choice is displayed as $4.99/month.
- [x] Annual prototype choice is displayed as $39.99/year.
- [x] Choosing either option enables Plus in local prototype storage.
- [x] Plus displays unlimited listings.
- [x] Plus removes the two-listing creation limit.
- [x] Profile displays Beau Dog Plus after the prototype upgrade.
- [x] Beau Dog does not take a percentage of rental payments; renter and owner arrange payment directly.

## QA findings / follow-up before production

1. **Real billing is still required before launch.** Current Plus buttons enable the plan locally for prototype testing only.
2. **Subscription status must eventually come from Apple/web billing rather than localStorage.**
3. **Restore Purchases / restore subscription access is required for the production iOS subscription flow.**
4. **Cancellation, expiration and renewal states must be handled by the production subscription system.**
5. **The upgrade screen currently returns to the equipment list after enabling Plus.** A later UX polish should let an owner continue directly into creating the third listing.
6. **A prototype-only Free/Plus test switch would make repeated QA easier without erasing all app data.** Do not ship that switch in production.

## Current result

The prototype correctly enforces the agreed launch model: Free users can list up to two items; Beau Dog Plus unlocks unlimited listings at the displayed $4.99/month or $39.99/year prototype price. Production billing remains a launch blocker.