---
name: Check Ergon Energy Retail CDR availability before calling
description: >-
  Poll Ergon Energy Retail's mandated Consumer Data Right status and outage
  endpoints to decide whether to call, retry or back off. These are the only two
  anonymous endpoints served on an Energy-Queensland-controlled host, and they
  are the provider's entire status surface — there is no human status page.
api: openapi/energy-queensland-cds-common-openapi.yml
base_url: https://public.cdr.ergonretail.com.au/cds-au/v1
auth: none
operations:
  - getStatus
  - getOutages
generated: '2026-07-27'
method: generated
---

# Check Ergon Energy Retail CDR availability before calling

Every CDR data holder must serve two unauthenticated Data Holder Operations
endpoints on its registered `publicBaseUri`. For Ergon Energy Retail that URI is
`https://public.cdr.ergonretail.com.au` — published in the ACCC CDR Register and
confirmed live on 2026-07-27. Check these before and during any batch of calls;
they are cheap, anonymous, and are the contractual signal a data recipient is
expected to honour.

## Step 1 — status (`getStatus`)

```
GET /discovery/status
x-v: 1
```

```json
{"data":{"status":"OK","updateTime":"2026-07-27T20:23:06Z","explanation":"All services operational"},
 "links":{"self":"https://public.cdr.ergonretail.com.au/cds-au/v1/discovery/status"},"meta":{}}
```

`data.status` is one of:

| Value | Meaning | What to do |
|---|---|---|
| `OK` | Implementation fully functional | Proceed |
| `PARTIAL_FAILURE` | One or more endpoints unexpectedly unavailable | Proceed cautiously; expect failures. `detectionTime` and `expectedResolutionTime` may be present |
| `SCHEDULED_OUTAGE` | An advertised outage is in effect | Do not call; check `getOutages` for the window |
| `UNAVAILABLE` | Whole implementation unexpectedly down | Back off and retry later |

`explanation` is mandatory whenever status is anything other than `OK`.

## Step 2 — outages (`getOutages`)

```
GET /discovery/outages
x-v: 1
```

Returns `data.outages[]`, each with `outageTime`, `duration`,
`isPartial` and `explanation`. As of 2026-07-27 the array is empty. Under the
Consumer Data Standards non-functional requirements, planned outages must be
published to data recipient software products with at least **one week** of lead
time (except for critical service or security fixes), so this endpoint is a
genuine forward-looking schedule rather than a post-hoc log.

## Availability context

- Obligation: **99.5% availability per calendar month**, covering authenticated *and* unauthenticated endpoints. Planned outages are excluded from the calculation.
- `Get Status` and `Get Outages` are classed **High Priority**: 95% of calls per hour must respond within **1000ms**.
- AEMO unavailability (the CDR secondary data holder for usage, DER and service point data) does *not* count against Ergon's availability, but will still make those requests fail.

## Errors

Both endpoints require `x-v`. Version failures return the standard CDS envelope,
e.g. `406 urn:au-cds:error:cds-all:Header/UnsupportedVersion` with detail
`Unable to locate a version of ResponseCommonDiscoveryStatus that is between
version 99 and 99`. Match on `code`, never on `detail`.

## Do not confuse this host with the plan host

`https://public.cdr.ergonretail.com.au` serves **only** these two endpoints
anonymously. `/cds-au/v1/energy/plans` returns an nginx 404 there — generic plan
data lives on the AER's Energy Made Easy host at
`https://cdr.energymadeeasy.gov.au/ergon/cds-au/v1`. See
`skills/energy-queensland-read-ergon-tariff-plans.md`.
