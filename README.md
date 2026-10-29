# char.gy

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

char.gy is a British public electric-vehicle charge point operator that specialises in on-street charging for the roughly forty percent of UK households with no off-street parking, and it is best known for putting the charger inside the lamp post. Founded by Richard Stobart out of the digital agency Unboxed, it installed its first public charger in Marlow, Buckinghamshire in 2018, is now led by CEO John Lewis from Floor 5, 55 King William St, London EC4R 9AD, and is backed with £100m by Zouk Capital through the UK Government-backed Charging Infrastructure Investment Fund. Its own about page claims over 5,000 charge points and 28.3 million kg of CO2 saved, and its live open data feed returned an x-total-count of 5,409 locations on 2026-07-27. In the UK energy value chain it sits at the very end of the wire: it is not a licensed supplier, not a network operator and not a metering agent, it operates charge points on street furniture owned by local authorities — Haringey, Southwark, Brent, Barnet, Harrow, Coventry, Brighton and Hove, Richmond and Wandsworth, Enfield and others — authorising drivers, metering the session and pricing it. Britain has no consumer data-portability mandate for energy equivalent to Australia's Consumer Data Right, so nothing compels char.gy to expose an individual driver's usage or billing data through an API, and it does not: there is no consumer API, no OAuth server, no OpenID Connect discovery document and no accredited-recipient scheme anywhere on the domain. What Britain DID mandate here is open infrastructure data. The Public Charge Point Regulations 2023 (SI 2023/1168), Part 4 regulation 10(5), require every charge point operator to make reference data and availability data available to the public free of charge, in a machine readable format, and — the crucial clause — "without any requirement to agree to terms and conditions regarding the use of that data". char.gy complies, and the compliance is real rather than claimed: it publishes an OCPI-shaped Locations feed and an OCPI-shaped Tariffs feed at https://char.gy/open-ocpi/locations and https://char.gy/open-ocpi/tariffs, both of which returned HTTP 200 with application/json to a completely anonymous GET on 2026-07-27, paginated with x-total-count, x-limit and RFC 5988 Link rel="next" headers, carrying real GB*CGY*E*NNNNN EVSE identifiers, IEC 62196 Type 2 connectors, per-connector tariff_ids and time-of-day restricted pence-per-kWh price components. The posture is therefore the clean split this sector keeps producing, but rotated: market and infrastructure data wide open and genuinely ungated because a regulation forbids gating it, consumer data entirely absent because no regulation asks for it, and the commercial OCPI CPO roaming interface at /ocpi/cpo/ closed behind OCPI Token authorization for partner e-mobility service providers. There is no developer portal — the entire public documentation for the open API is a single Freshdesk help-centre article.

**Areas:** Energy · United Kingdom · EV Charging · Electricity · Utilities · OCPI · Charge Point Operator · Open Data · Roaming · Tariffs · Mobility · Electrification

## char.gy on APIs.io

Everything profiled for char.gy is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/chargy/](https://apis.io/providers/chargy/)** — or go straight to one of the APIs or properties below.

### APIs (3)

- [char.gy OCPI CPO Roaming API](https://apis.io/apis/chargy/chargy-ocpi-cpo-api/) — char.gy's commercial Open Charge Point Interface implementation in the Charge Point Operator role, used so that another network's drivers can authorise,…
- [char.gy Locations API](https://apis.io/apis/chargy/chargy-locations-api/) — Reference and availability data for char.gy charge points.
- [char.gy Tariffs API](https://apis.io/apis/chargy/chargy-tariffs-api/) — Published price components for char.gy charging sessions.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [chargy](https://apis.io/servers/chargy/chargy/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Chargy Agentic Access](https://apis.io/agentic-access/chargy/chargy-agentic-access/)

#### Examples (2)

Example requests and responses.

- [Chargy Locations Response](https://apis.io/examples/chargy/chargy-locations-response/)
- [Chargy Tariffs Response](https://apis.io/examples/chargy/chargy-tariffs-response/)

#### Collections (1)

Postman and Open Collection request collections.

- [char.gy Open Charge Point Data API](https://apis.io/collections/chargy/open-chargy-open-charge-point-data/)

#### Overlays (1)

OpenAPI overlays, including conversational phrasing for each operation.

- [Chargy Open Charge Point Data Overlay](https://apis.io/overlays/chargy/chargy-open-charge-point-data-overlay/)

#### Security (2)

Authentication, trust centre, and vulnerability disclosure.

- [Chargy Authentication](https://apis.io/security/chargy/chargy-authentication/)
- [Chargy Domain Security](https://apis.io/security/chargy/chargy-domain-security/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://char.gy/)
- [Documentation](https://help.char.gy/support/solutions/articles/77000576948-public-charge-point-regulations-2023)
- [Pricing](https://char.gy/us/pricing)
- [Sign up](https://char.gy/users/payg_registrations/new)
- [Support](https://help.char.gy/)
- [Blog](https://char.gy/us/news)
- [Compliance](https://help.char.gy/support/solutions/articles/77000576948-public-charge-point-regulations-2023)
- [Terms of service](https://char.gy/us/terms-of-use)
- [Privacy policy](https://char.gy/us/privacy-notice)
- [GitHub](https://github.com/char-gy)

## API Evangelist rating

**Kin Score 33.1** — thin · rubric 0.24.0 · scored 2026-10-17

| Facet | Score |
|---|---|
| Discoverability | 66.1 |
| Contract quality | 16.3 |
| Contract governance | 18.2 |
| Operational transparency | 2.6 |
| Developer ergonomics | 30.4 |
| Access clarity | 52.6 |

**Agent readiness 30.2** — agent-ready

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | na |
| MCP Server | — |
| Auth Clarity | bearer (partial credit) |
| Idempotency | na |
| Error Semantics | documented (partial credit) |
| OpenAPI Examples | verified |
| Rate Limit Signal | — |
| Event Surface Described | — |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | na |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |

**Regulatory alignment 35.2** — Energy & Utilities

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/chargy/](https://apis.io/providers/chargy/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for char.gy: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/chargy/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
