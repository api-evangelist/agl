---
name: Publish golf club tee times to AGL as a supplier
description: Register a golf club, publish daily tee times with pricing and refund policy, and
  correct a published tee time using the AGL OPEN API supplier bridge.
api: openapi/agl-open-openapi-original.yml
base_url: https://agl-bridgeapi.tigergds.com
operations:
  - POST /api/golfclub
  - GET /api/golfclub/list
  - POST /api/teetime/daily
  - GET /api/teetime/list
  - PUT /api/teetime/availability
generated: '2026-09-12'
method: generated
source: openapi/agl-open-openapi-original.yml (harvested from https://api-docs-agl-bridgeapi.tigergds.com/reference)
---

# Publish golf club tee times to AGL as a supplier

The supplier side of TIGER GDS. Base URL `https://agl-bridgeapi.tigergds.com`. The specification
declares no `operationId`s, so steps name the method and path verbatim.

## Before you start

- Every `SupplierToAGL` call needs `Authorization: Bearer <SHA-256 hashed signature>` **and**
  `X-Supplier-Code: <code issued by AGL>`. The canonical string that gets hashed is **not
  published** — get it from AGL during onboarding.
- Responses are `{isSuccess, rstCd, rstMsg, statusCode}`. `rstCd` is `SUCCESS` on the happy path
  and `INVALID_INPUT` on the documented 400.
- The spec declares a sandbox host, `https://sandbox-agl-bridgeapi.tigergds.com`. **It did not
  resolve when probed on 2026-09-12** — confirm with AGL before planning a test cycle against it.
- No idempotency key exists. Re-posting a golf club or a daily tee time is not safe to retry blind.

## Steps

1. **Register the club.** `POST /api/golfclub` with the `GolfClub` body: `golfClubCode`,
   `golfClubName`, `address`, `countryCode`, `currency`, `language`, `latitude`, `longitude`,
   `email`, `fax`, `homepage`, `description`, `images`, `isGuestInfoRequired`, `courses[]`
   (`courseCode`, `courseName`, `courseHoleCount`, `startHole`) and `holeInfo[]` (`holeNumber`,
   `holeName`, `par`, `distance`, `distanceUnit`). **There is no delete or deactivate operation for
   a registered club** — this write has no reversal path in the contract.
2. **Verify it landed.** `GET /api/golfclub/list` with the required `golfClubCode`, `startDate` and
   `endDate` (`yyyy-MM-dd`, filtering on registration date).
3. **Publish tee times.** `POST /api/teetime/daily` with `golfClubCode` and `teeTimeDailyInfo[]`.
   Each entry carries `courseCode`, `playDate`, `timeDaily[]` (`startTime`, `teeTimeCode`),
   `minPlayers`/`maxPlayers`, `includeCaddie`, `includeCart`, `reservationType`, a `price` block
   (`greenFee`, `caddieFee`, `cartFee`, `tax`, `additionalTax`, `unitPrice`, `playerCount`) and a
   `refundPolicy[]` (`refundDate`, `refundFee`, `refundUnit`) — the refund policy is what governs
   how a booking against this tee time can later be reversed, so set it deliberately.
4. **Check what AGL holds.** `GET /api/teetime/list`.
5. **Correct a tee time — the two-step, because there is no update.** AGL states it plainly in the
   contract: *"There is no API for directly updating an existing tee time (e.g., price, time, or
   policy)."* The official workflow is:
   a. `PUT /api/teetime/availability` with `availability[]` (`golfClubCode`, `courseCode`,
      `playDate`, `time`, `available: false`). **Omitting the filters applies globally** — always
      send the narrowest filter you mean.
   b. `POST /api/teetime/daily` again, registering the corrected tee time as a new entry.

## Receiving bookings

The same specification's `AGLToSupplier` tag describes two operations **you implement and AGL
calls** — see `asyncapi/agl-webhooks.yml`:

- `POST /reservation` — AGL sends a `ReservationRequest` (`golfClubCode`, `courseCode`,
  `reservationDate`, `reservationStartTime`, `holderName`, `reservationMembers`, `guestInfo`,
  `reservationEmail`, `reservationPhone`, `reservationCountry`, `currency`, `totalPrice`). Reply
  with `ReservationResponse` including your `reservationId`.
- `POST /reservation/cancel` — AGL sends `{reservationId}`. Reply with `CancelResponse`.

These calls carry `Authorization: Bearer <SHA-256 hashed signature>` and `X-Client-Code`, the code
**you** issue to AGL. AGL does not publish the signing canonicalization, retry policy or delivery
ordering, so agree all three during onboarding.
