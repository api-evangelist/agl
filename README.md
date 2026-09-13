# AGL

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

AGL Inc. (에이지엘) is a Seoul-headquartered golf technology company, founded in 2019, that operates
**TIGER GDS** — a global distribution system for golf. Its SaaS platform connects golf club tee-time
inventory to travel and booking channels in real time across more than 1,000 contracted courses in
30+ countries, and is the system behind the HeyTeeTime / TIGERBOOKING consumer apps and the Reserve
with Google golf integration. Offices in Seoul, Tokyo, Brea (California) and Singapore.

## What AGL publishes

Three machine-readable REST contracts, all served from `tigergds.com`:

| API | Spec | Ops | Docs |
|---|---|---|---|
| AGL OTA API 2.0 | OpenAPI 3.1.1 | 24 | <https://api-doc.tigergds.com/reference> |
| AGL OPEN API 0.0.1 (supplier bridge) | OpenAPI 3.1.1 | 7 | <https://api-docs-agl-bridgeapi.tigergds.com/reference> |
| AGL Trip.com Reservation Integration API 1.0 | OpenAPI 3.0.1 | 1 | <https://outboundapi-trip-reserv.tigergds.com/swagger/index.html> |

None of these is linked from `aglgw.com`, which advertises "API method — Direct API integration"
on its Golf Club and Partner Channel pages and routes every reader to a partnership form. The
contracts were found through certificate transparency on `tigergds.com` and are publicly readable.

## Notes for an integrator

- **HTTP 200 is not success on the OTA API.** It declares only `200` responses; failures come back
  as `CommonResponse.status == "fail"` with codes `FL00`, `FL01` or `ET00` — two of which the
  specification never defines.
- **No idempotency key** on any of the ten mutating operations.
- **Reversal is well covered and the window is data**: `POST /v2/reservation/request` returns a
  `CancellationPolicy` whose tiers carry `appliesUntil` cut-offs and fee percentages.
- **Tee times cannot be updated** — AGL's own contract says so; set unavailable, then re-register.
- **The declared sandbox does not exist**: the AGL OPEN API lists
  `https://sandbox-agl-bridgeapi.tigergds.com` as its Sandbox Environment and the host returns
  NXDOMAIN (probed 2026-09-12).
- No published rate limits, status page, deprecation policy, changelog, SDK, CLI, MCP server or
  A2A agent card.

Everything in this repository was assembled from those public surfaces. See `apis.yml` for the
full artifact index.
