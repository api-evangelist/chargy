# char.gy (chargy)

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

char.gy is a British public electric-vehicle charge point operator that specialises in on-street charging for the roughly forty percent of UK households with no off-street parking, and it is best known for putting the charger inside the lamp post. Founded by Richard Stobart out of the digital agency Unboxed, it installed its first public charger in Marlow, Buckinghamshire in 2018, is now led by CEO John Lewis from London, and is backed with £100m by Zouk Capital through the UK Government-backed Charging Infrastructure Investment Fund. In the UK energy value chain it sits at the very end of the wire — not a licensed supplier, not a network operator, not a metering agent — operating charge points on street furniture owned by local authorities. Britain has no consumer data-portability mandate for energy, so char.gy exposes no consumer API at all. What Britain did mandate is open infrastructure data, and char.gy implements it for real: an anonymous, ungated OCPI-shaped Locations and Tariffs feed carrying 5,409 charge point locations.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/chargy/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/chargy/refs/heads/main/apis.yml)

## Tags

- Energy
- United Kingdom
- EV Charging
- Electricity
- Utilities
- OCPI
- Charge Point Operator
- Open Data
- Roaming
- Tariffs
- Mobility
- Electrification

## Timestamps

- **Created:** 2026-07-27
- **Modified:** 2026-07-27

## APIs

### char.gy Open Charge Point Data API

char.gy's statutory open data feed, published to satisfy Part 4 regulation 10 of the UK Public Charge Point Regulations 2023, which requires reference data and availability data to be made available to the public free of charge, in a machine readable format, and without any requirement to agree to terms and conditions. It is shaped as an Open Charge Point Interface (OCPI) surface with exactly two modules exposed, both read-only GET and both completely unauthenticated. `GET /open-ocpi/locations` returned HTTP 200 and `application/json` anonymously on 2026-07-27 with the OCPI envelope, an `x-total-count` of 5409 locations, a default `x-limit` of 50, and an RFC 5988 `Link` header advertising `rel="next"`. `GET /open-ocpi/tariffs` returned HTTP 200 with 3 tariff objects including a real time-of-day GBP price structure. No `/open-ocpi/versions` endpoint is served, and the sessions, cdrs, tokens, commands and credentials modules are all 404 — the open surface is exactly the size of the statute.

- **Human URL:** [https://help.char.gy/support/solutions/articles/77000576948-public-charge-point-regulations-2023](https://help.char.gy/support/solutions/articles/77000576948-public-charge-point-regulations-2023)
- **Base URL:** `https://char.gy/open-ocpi`

#### Tags

- Open Data
- EV Charging
- OCPI
- Locations
- Tariffs
- Charge Point Operator
- United Kingdom

#### Properties

- [Documentation](https://help.char.gy/support/solutions/articles/77000576948-public-charge-point-regulations-2023)
- [Specification](https://github.com/ocpi/ocpi) — Open Charge Point Interface
- [Legal](https://www.legislation.gov.uk/uksi/2023/1168/regulation/10/made) — Public Charge Point Regulations 2023, reg. 10
- [Terms of Service](https://char.gy/us/terms-of-use)
- [Support](https://help.char.gy/)

### char.gy OCPI CPO Roaming API

char.gy's commercial Open Charge Point Interface implementation in the Charge Point Operator role, used so that another network's drivers can authorise, charge and be settled on char.gy infrastructure. char.gy publishes no documentation for it. Its existence was established from `robots.txt`, which explicitly disallows `/ocpi/`, `/api/` and `/webhooks/`, and confirmed by anonymous probes returning HTTP 401 with `www-authenticate: Token realm="OCPI"` on the versions, locations, tariffs, sessions, cdrs and credentials paths, while control paths returned 404. `GET /ocpi/cpo/2.2/credentials` returned HTTP 200 with `{"status_code":3002,"status_message":"Unsupported version"}` while 2.2.1 and 2.1.1 returned 401 — placing the roaming interface on OCPI 2.2.1 and 2.1.1. Access is partner-only via a commercial roaming agreement and an OCPI credentials handshake.

- **Human URL:** [https://char.gy/us/partners](https://char.gy/us/partners)
- **Base URL:** `https://char.gy/ocpi/cpo`

#### Tags

- EV Charging
- OCPI
- Roaming
- Charge Point Operator
- Sessions
- CDRs
- United Kingdom

#### Properties

- [Specification](https://github.com/ocpi/ocpi) — Open Charge Point Interface
- [Partners](https://char.gy/us/partners)
- [Support](https://help.char.gy/)
- [Terms of Service](https://char.gy/us/terms-of-use)

## Common Properties

- [Website](https://char.gy/)
- [Documentation](https://help.char.gy/support/solutions/articles/77000576948-public-charge-point-regulations-2023)
- [About](https://char.gy/us/about)
- [Products](https://char.gy/us/our-products-ev-charging)
- [Partners](https://char.gy/us/partners)
- [Drivers](https://char.gy/us/drivers)
- [Pricing](https://char.gy/us/pricing)
- [Blog](https://char.gy/us/news)
- [Support](https://help.char.gy/)
- [Contact](https://char.gy/us/contact-us)
- [Privacy](https://char.gy/us/privacy-notice)
- [Terms of Service](https://char.gy/us/terms-of-use)
- [LinkedIn](https://www.linkedin.com/company/char.gy)
- [Application — iOS](https://apps.apple.com/app/1636840750)
- [Application — Android](https://play.google.com/store/apps/details?id=com.chargy_limited.driverapp)

## Mandate Posture

| Field | Value |
| --- | --- |
| Mandate regime | `other` — Public Charge Point Regulations 2023 (SI 2023/1168), Part 4, reg. 10 |
| Mandate status | `live-implemented` — endpoints called anonymously, HTTP 200, 5,409 records |
| Data standard | OCPI (Locations + Tariffs), version undeclared on the open feed |
| Consumer data API | No — Britain has no energy consumer data-portability right |
| Market data open | Yes — fully anonymous, ungated, because reg. 10(5) forbids gating it |
| Access gate | `self-serve` — no key, no account, no terms to accept |
| Auth model | None on the open feed; OCPI `Token` on the gated CPO roaming interface |
| Home market | United Kingdom |

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
