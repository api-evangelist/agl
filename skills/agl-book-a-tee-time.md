---
name: Book a golf tee time through AGL TIGER GDS
description: Search AGL's golf club catalogue, find an open tee time, hold it, read the
  cancellation ladder, and confirm with payment using the AGL OTA API v2.
api: openapi/agl-ota-openapi-original.yml
base_url: https://gw-ota.tigergds.com
operations:
  - GET /v2/codes/countries
  - GET /v2/golfClubs
  - GET /v2/golfClub
  - GET /v2/teeTime/openDates
  - GET /v2/teeTime/openTeeTimes
  - POST /v2/reservation/request
  - POST /v2/reservation/confirm
  - GET /v2/reservation
  - POST /v2/reservation/sendVoucher
generated: '2026-09-12'
method: generated
source: openapi/agl-ota-openapi-original.yml (harvested from https://api-doc.tigergds.com/reference)
---

# Book a golf tee time through AGL TIGER GDS

The AGL OTA API declares **no `operationId`s**, so every step below names the exact HTTP method and
path from the specification. Base URL `https://gw-ota.tigergds.com`.

## Before you start

- Send `Authorization: <token>` **and** `clientId: <your AGL-issued client id>` on every request.
  Both are declared as apiKey-in-header schemes and both are applied globally.
- `language` (`ko|en|ja|es|zh|tw`) and `currency` (e.g. `KRW`) are **required query parameters on
  every read operation**. A missing one is the failure the spec itself exemplifies
  ("One of required parameter is missing.").
- **HTTP 200 does not mean success.** Every response is a `CommonResponse` envelope; branch on
  `status`, which is `"ok"` or `"fail"`. On failure read `statusDescription` — the symbolic codes
  are `FL00`, `FL01`, `ET00` and the specification does not define what distinguishes them.
- **There is no idempotency key.** Never blind-retry a write: a repeated
  `POST /v2/reservation/request` creates a second hold on inventory.

## Steps

1. **Resolve the geography codes.** `GET /v2/codes/continents`, then `GET /v2/codes/countries`
   (by continent), then `GET /v2/codes/regions` or `GET /v2/codes/cities` (by country). Airports are
   at `GET /v2/codes/airports`, facility codes at `GET /v2/codes/facilities`.
2. **Find candidate clubs.** `GET /v2/golfClubs` with `codeType` (`continent|country|region|city|
   airport|facility`) and `codeValues` (comma-joined, e.g. `a,e`). This returns summaries only —
   `id`, `name`, `currency`, `minPrice`, `minPriceDate`, `timezone`, `category`, `lastUpdateAt`.
3. **Read the club.** `GET /v2/golfClub` for the detail: `cntHoles`, `par`, `courseLength`,
   `address`, `latitude`/`longitude`, `googlePlaceId`, `courses` with per-hole cards, `facilities`,
   and the `GolfClubInformation` block (`includedItems`, `excludedItems`, `cancellationPolicy`,
   `important`).
4. **Find dates, then times.** `GET /v2/teeTime/openDates` for the club, then
   `GET /v2/teeTime/openTeeTimes` with `golfClubId` and `openDate` (ISO date). The response is
   `data.courses[]`, each with `teeTimes[]`.
5. **Hold the tee time.** `POST /v2/reservation/request`. Only one reservation request can be made
   at a time; if you are adding to an existing booking, include the existing integrated
   reservation number in `reservationNumber`. The response returns `reservationId`,
   `reservationNumber` (the integrated group key) and — the part that matters — a
   `cancellationPolicy`.
6. **Read the cancellation ladder before you pay.** `cancellationPolicy.policies[]` is an ordered
   set of `{amountType, amount, appliesUntil}` tiers, where `amountType` is `cancellationFee` or
   `cancellationFeePerc` and `appliesUntil` is the cut-off. The published example is 50% until
   `2025-02-22 11:00`, then 100%. Surface these numbers to the user before step 7. *(Note the
   example format is `YYYY-MM-DD HH:mm` with no zone designator even though the field is described
   as UTC.)*
7. **Confirm and pay.** `POST /v2/reservation/confirm` with `reservationNumber` and a `payment`
   object (`currency`, `totalAmount`, `amountLines`, `mobile`, `email`, `paymentMethod`). This is
   the irreversible-by-default step — after it, cancelling costs whatever the ladder in step 6 says.
8. **Verify.** `GET /v2/reservation?reservationNumber=…` returns the `Reservation` with
   `payment`, `charge` amounts and the constituent `reservations[]`.
9. **Deliver the voucher.** `POST /v2/reservation/sendVoucher` with `reservationNumber`. It returns
   no data. Sending is not retractable.

## If the user changes their mind

- Before confirm: `DELETE /v2/reservation/request` (one request, by `reservationId`) or
  `DELETE /v2/reservation/requests` (the whole group, by integrated reservation number).
- After confirm: `DELETE /v2/reservation` (whole) or `POST /v2/reservation/partialcancel?
  reservationId=…` (part). Quote the applicable tier from step 6 first.

## What this API will not do

No pagination (narrow the filter instead), no webhooks or status callbacks on the OTA side (poll
`GET /v2/reservation`), no rate-limit headers, and no sandbox.
