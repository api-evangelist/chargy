# char.gy (chargy)

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
