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

AGL Inc. (에이지엘) is a Seoul-headquartered golf technology company, founded in 2019, that operates TIGER GDS — a global distribution system for golf. Its SaaS platform connects golf club tee-time inventory to travel and booking channels in real time, covering more than 1,000 contracted golf courses across 30+ countries, and is the system behind the HeyTeeTime/TIGERBOOKING consumer apps and the Reserve with Google golf integration. AGL publishes three machine-readable REST contracts on tigergds.com: the AGL OTA API (distribution — code lookups, golf club catalog, tee-time availability, static packages and the full reservation lifecycle), the AGL OPEN API (a bi-directional supplier bridge for golf-club and tee-time registration plus reservation callbacks) and a Trip.com outbound reservation integration. Offices in Seoul, Tokyo, Brea (CA) and Singapore.

**Areas:** Company · Golf · Travel · Booking · Reservations · Distribution · Tee Times · GDS · Hospitality · Sports · Leisure · South Korea

## AGL on APIs.io

Everything profiled for AGL is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/agl/](https://apis.io/providers/agl/)** — or go straight to one of the APIs or properties below.

### APIs (8)

- [AGL AGL To Supplier API](https://apis.io/apis/agl/agl-agltosupplier-api/) — APIs where AGL sends reservation and cancellation requests to suppliers
- [AGL Codes API](https://apis.io/apis/agl/agl-codes-api/) — The Codes API from AGL — 9 operation(s) for codes.
- [AGL Golf Clubs API](https://apis.io/apis/agl/agl-golf-clubs-api/) — The Golf Clubs API from AGL — 2 operation(s) for golf clubs.
- [AGL Reservation API](https://apis.io/apis/agl/agl-reservation-api/) — The Reservation API from AGL — 1 operation(s) for reservation.
- [AGL Reservations API](https://apis.io/apis/agl/agl-reservations-api/) — The Reservations API from AGL — 6 operation(s) for reservations.
- [AGL Static Packages API](https://apis.io/apis/agl/agl-static-packages-api/) — The Static Packages API from AGL — 2 operation(s) for static packages.
- [AGL Supplier To AGL API](https://apis.io/apis/agl/agl-suppliertoagl-api/) — APIs where suppliers send data to AGL (e.g., golf club registration, tee times, etc.)
- [AGL Tee Times API](https://apis.io/apis/agl/agl-tee-times-api/) — The Tee Times API from AGL — 2 operation(s) for tee times.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### AsyncAPI (1)

Event-driven and webhook contracts.

- [Agl Webhooks](https://apis.io/asyncapis/agl/agl-webhooks/)

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [agl-tiger-gds](https://apis.io/servers/agl/agl-tiger-gds/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Agl Agentic Access](https://apis.io/agentic-access/agl/agl-agentic-access/)

#### Overlays (3)

OpenAPI overlays, including conversational phrasing for each operation.

- [Agl Open Overlay](https://apis.io/overlays/agl/agl-open-overlay/)
- [Agl Ota Overlay](https://apis.io/overlays/agl/agl-ota-overlay/)
- [Agl Tripcom Outbound Overlay](https://apis.io/overlays/agl/agl-tripcom-outbound-overlay/)

#### Security (2)

Authentication, trust centre, and vulnerability disclosure.

- [Agl Authentication](https://apis.io/security/agl/agl-authentication/)
- [Agl Domain Security](https://apis.io/security/agl/agl-domain-security/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Agl Plans Pricing](https://apis.io/plans/agl/agl-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Agl Rate Limits](https://apis.io/rate-limits/agl/agl-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://www.aglgw.com/en/)
- [Documentation](https://api-doc.tigergds.com/reference)
- [API reference](https://api-doc.tigergds.com/reference)
- [Sign up](https://www.tigergds.com/signup/step1)
- [Support](https://www.aglgw.com/en/partners)
- [Blog](https://www.aglgw.com/en/contents/news)
- [GitHub](https://github.com/aglgw)

## API Evangelist rating

**Kin Score 31.2** — thin · rubric 0.24.0 · scored 2026-10-17

| Facet | Score |
|---|---|
| Discoverability | 71.4 |
| Contract quality | 55.1 |
| Contract governance | 4.5 |
| Operational transparency | 10.5 |
| Developer ergonomics | 37.5 |
| Access clarity | 6.6 |

**Agent readiness 35.0** — agent-ready

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | documented (partial credit) |
| MCP Server | — |
| Auth Clarity | bearer (partial credit) |
| Idempotency | — |
| Error Semantics | verified |
| OpenAPI Examples | partial |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | yes |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |

**Regulatory alignment 16.7** — Horizontal (data, software, accessibility, platform)

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/agl/](https://apis.io/providers/agl/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for AGL: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/agl/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
