---
name: Keep a local mirror of the char.gy open charge point dataset in sync
description: >-
  Perform an initial full crawl of the char.gy statutory open data feed and then
  keep it current with incremental date_from syncs, without a credential and
  without re-downloading 5,409 locations every run.
api: openapi/chargy-open-charge-point-data-openapi.yml
operations: [listLocations, listTariffs]
generated: '2026-07-27'
method: generated
---

# Keep a local mirror of the char.gy open charge point dataset in sync

The char.gy feed is a regulated public dataset — free, anonymous, and stable in
shape but with no version, no changelog and no SLA. Mirroring it is the right
pattern for anything that queries it more than occasionally, because the API
offers no way to ask a targeted question.

## Initial full crawl

1. `listTariffs` — `GET /open-ocpi/tariffs`. One request, 3 objects. Store them
   keyed by `id`.
2. `listLocations` — `GET /open-ocpi/locations?limit=50&offset=0`, then follow
   the `Link` header `rel="next"` until it is absent. `x-total-count` (5,409 on
   2026-07-27) tells you how many to expect; `x-limit` confirms the page size
   actually applied.
3. Stop when `data` comes back empty **or** the `Link` header has no `rel="next"`.
   Both are valid terminators; an over-the-end offset returns `200` with an
   empty array, not a 404.
4. Record the crawl start time in UTC ISO 8601. That timestamp is your
   watermark.

Store `last_updated` per location — it is the change key.

## Incremental sync

`GET /open-ocpi/locations?date_from=<watermark>&limit=50&offset=0`, paging as
before, then advance the watermark to the new crawl start time.

`date_from` filters on `last_updated` and is genuinely implemented: a same-day
watermark cut the result from 5,409 to 2,396 objects on 2026-07-27, and a future
watermark returned 0. `date_to` also works (a `date_to` of 2026-07-01 returned
6 objects), which is useful for backfilling a window.

Caveat: **this feed exposes no deletions.** A location that is removed simply
stops appearing in the full listing; an incremental sync will never tell you it
went away. Do a full crawl periodically — weekly is proportionate for a
5,000-object dataset — and reconcile disappearances.

Re-fetch `/open-ocpi/tariffs` on every sync. It is one request and tariff
`last_updated` moves independently of locations.

## Validate every response

- `status_code` must be `1000`. Anything in the 2xxx range is a client error
  delivered with an HTTP **200** — `2001` is what you get for a malformed
  `limit` or `date_from`. Never trust the status line alone.
- `3002` ("Unsupported version") belongs to the commercial CPO surface, not
  this one.
- Persist `x-request-id` alongside failures. It is the only diagnostic handle
  support@char.gy has, and there is no status page to check against
  (status.char.gy does not resolve).

## Schema stability expectations

There is no version negotiation on this feed — `GET /open-ocpi/versions` returns
404 — and no changelog, so shape changes will arrive unannounced. Defend
accordingly:

- Treat `owner` as optional. It was absent on roughly 40% of a 250-record
  sample.
- Treat `evse.status` as an open string set. `WORKING` and `FAULTED` are what
  char.gy sends today; neither is an OCPI 2.2.1 value, so do not validate
  against the OCPI enumeration.
- `coordinates.latitude` / `.longitude` are **strings**, not numbers.
- Do not assume tariff `currency` is GBP.

## Licensing

There is no licence page and no terms gate on this data, deliberately:
regulation 10(5) of the Public Charge Point Regulations 2023 requires it to be
available "without any requirement to agree to terms and conditions regarding
the use of that data". Attribute char.gy as the operator (`operator.name` in
every record) as good practice.
