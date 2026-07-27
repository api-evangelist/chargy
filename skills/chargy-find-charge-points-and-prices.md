---
name: Find char.gy charge points and what they cost
description: >-
  Crawl the char.gy statutory open data feed to answer questions about where UK
  on-street lamp-post chargers are, whether they are working, and what a kWh
  costs at a given time of day. No credential is required.
api: openapi/chargy-open-charge-point-data-openapi.yml
operations: [listLocations, listTariffs]
generated: '2026-07-27'
method: generated
---

# Find char.gy charge points and what they cost

char.gy publishes 5,409 UK on-street charge point locations and 3 tariffs at
`https://char.gy/open-ocpi`, with **no authentication of any kind**. That is not
generosity; regulation 10(5) of the Public Charge Point Regulations 2023 makes
gating this data unlawful. Send no `Authorization` header — there is nothing to
send.

## 1. Get the tariffs first (they are tiny)

`listTariffs` — `GET /open-ocpi/tariffs`

Three objects, one page. Index them by `id`. Each `Tariff` has `elements[]`,
each element has `price_components[]` (only `type: ENERGY` is used — price per
kWh in `currency`) and an optional `restrictions` block with `start_time`,
`end_time` and `day_of_week[]`.

To price a session you must evaluate the restrictions yourself: an element with
**no** `restrictions` applies always; the GBP tariff uses three elements to
express weekday off-peak (00:00–07:00 Mon–Fri), weekday peak (07:00–00:00
Mon–Fri) and weekend. Times are `Europe/London`, per the location's `time_zone`.

Do not assume GBP. Tariff records with `currency` EUR and USD are published on
the same GB/CGY party. Read `currency` before you quote a price.

## 2. Page the locations

`listLocations` — `GET /open-ocpi/locations?limit=50&offset=0`

- Default page size is 50 (`x-limit`); total is in `x-total-count`; follow the
  `Link` header `rel="next"` until it is absent. A full crawl is ~109 requests
  at the default page size.
- **There is no spatial, city, postcode or status filter.** Geographic questions
  require crawling everything and filtering client-side on `coordinates`,
  `city` or `postal_code`.
- For a refresh, do not re-crawl: pass `date_from=<timestamp of your last
  crawl>` to get only objects whose `last_updated` moved. This is verified
  working — it reduced the count from 5,409 to 2,396 for a same-day timestamp.

## 3. Join a charger to its price

`location.evses[].connectors[].tariff_ids[]` → `tariff.id`. That is the only
join in the model. There is no per-object endpoint: `GET /open-ocpi/locations/{id}`
returns 404, so you cannot look one location up directly — you find it in a page.

## 4. Read availability correctly

`evse.status` is **not** an OCPI status value. Observed values are `WORKING` and
`FAULTED`, which encode the regulator's binary "is it working" concept, not the
OCPI `AVAILABLE / CHARGING / INOPERATIVE` enumeration. Treat `WORKING` as
usable and `FAULTED` as not; do not map either onto OCPI semantics. Regulation
10(4) requires this field to update within 30 seconds of a change, so it is
fresh — but it tells you nothing about whether a working charger is currently
occupied.

## 5. Error handling — the trap

**Client errors arrive as HTTP 200.** A bad `limit` or an unparseable
`date_from` returns `200` with `{"status_code": 2001, "status_message": "Limit
is not a number"}` and **no `data` member**. A client that branches on the HTTP
status line will read a rejected request as an empty result set.

Check `status_code == 1000` on every response before touching `data`.

An `offset` past the end is *not* an error: it returns `200`, `status_code`
1000 and an empty `data` array. That is your stop condition alongside the
missing `Link` header.

## 6. Be polite

No rate limit is published and none is signalled (no `x-ratelimit-*`, no
`Retry-After`, no 429 observed). That is not permission to hammer it. Use
`date_from` for incremental syncs, honour the `etag`, and keep concurrency low.
Every response carries `x-request-id` — log it, it is the only correlation
handle support@char.gy has.

## Out of scope

Sessions, CDRs, tokens and commands are not here. They live on the
credential-gated OCPI CPO roaming interface at `/ocpi/cpo/`, which returns 401
with `www-authenticate: Token realm="OCPI"` and is partner-only. There is no
consumer API — no surface exposes an individual driver's own charging history
or billing to that driver.
