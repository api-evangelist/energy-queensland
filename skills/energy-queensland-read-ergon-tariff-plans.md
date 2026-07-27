---
name: Read Ergon Energy Retail tariff plans
description: >-
  Retrieve Ergon Energy Retail's regulated electricity plans for regional
  Queensland and the full tariff detail of any one of them, anonymously, with no
  key or signup. Handles the two things that trip callers up on a Consumer Data
  Right surface: the mandatory x-v version header, which differs per endpoint,
  and page-number pagination.
api: openapi/energy-queensland-cds-energy-openapi.yml
base_url: https://cdr.energymadeeasy.gov.au/ergon/cds-au/v1
auth: none
operations:
  - listEnergyPlans
  - getEnergyPlanDetail
generated: '2026-07-27'
method: generated
---

# Read Ergon Energy Retail tariff plans

Ergon Energy Retail is the notified-price electricity retailer for regional
Queensland and a designated Consumer Data Right energy data holder. Its generic
plan data is **public and anonymous** — no API key, no signup, no accreditation.
Note the host: in CDR energy, generic plan data is served centrally by the
Australian Energy Regulator's Energy Made Easy CDR host under a per-brand path,
**not** by the retailer. Requesting `/energy/plans` on Ergon's own base URI
returns an nginx 404, and that is correct behaviour, not an outage.

## Before you start

- Base URL: `https://cdr.energymadeeasy.gov.au/ergon/cds-au/v1`
- Every request **must** carry an `x-v` header naming the endpoint version. Omitting it returns `400 urn:au-cds:error:cds-all:Header/Missing` with detail `Header x-v must be provided`.
- The required version **differs per endpoint**: `listEnergyPlans` serves version 1 (max 1); `getEnergyPlanDetail` requires **minimum version 3**.
- Optionally send `x-fapi-interaction-id` as an RFC 4122 UUID; it is played back verbatim in the response for correlation.

## Step 1 — list the plans (`listEnergyPlans`)

```
GET /energy/plans?page-size=25&page=1
x-v: 1
```

Returns `data.plans[]` plus `links` (self/first/prev/next/last) and
`meta.totalRecords` / `meta.totalPages`. As of 2026-07-27 Ergon returns 36 plans,
all `type: REGULATED` and `fuelType: ELECTRICITY` — regulated rather than market
offers, because this retailer sells Queensland government notified prices.

Useful filter parameters on this operation: `type`, `fuelType`, `effective`,
`updated-since`, `brand`, `page`, `page-size`.

Each plan carries `planId` (e.g. `ERG1064038RRE1@EME`), `brand` (`ergon`),
`brandName`, `displayName`, `customerType`, `effectiveFrom`/`effectiveTo`,
`lastUpdated`, and a `geography` block listing the distributor (`Ergon`) and
several hundred regional Queensland postcodes.

## Step 2 — page through the whole set

Follow `links.next` until it is absent, or increment `page` up to
`meta.totalPages`. Rules that are enforced, not advisory:

- `page-size` maximum is **1000**; larger returns `400 urn:au-cds:error:cds-all:Field/InvalidPageSize`.
- A page beyond `meta.totalPages` returns **422** `urn:au-cds:error:cds-all:Field/InvalidPage` — note 422, not 404.
- A non-integer `page` returns `400 urn:au-cds:error:cds-all:Field/Invalid`.

## Step 3 — get the tariff detail (`getEnergyPlanDetail`)

```
GET /energy/plans/{planId}
x-v: 3
```

`x-v: 1` or `2` returns `406 urn:au-cds:error:cds-all:Header/UnsupportedVersion`
with detail `Header x-v lower than minimum supported [x-v=1, min=3]` — versions 1
and 2 of this endpoint were retired on 2024-09-09 and 2025-03-03 respectively.

The detail payload adds the `electricityContract` block: tariff periods
(single rate, time of use, demand charges, banded daily supply charges),
controlled load, solar feed-in tariffs, discounts, incentives, fees, eligibility
and metering charges.

## Error handling

Errors are **not** RFC 9457 problem+json. The envelope is:

```json
{"errors":[{"code":"urn:au-cds:error:cds-all:Header/UnsupportedVersion","title":"Unsupported Version","detail":"Header x-v greater than maximum supported [x-v=99, max=1]"}]}
```

Match on `code` (stable), not on `detail` (occurrence-specific, and worded
differently by the two hosts). Full catalogue: `errors/energy-queensland-problem-types.yml`.

## Rate limits and etiquette

Public unauthenticated traffic is capped at 300 TPS across all consumers under
the Consumer Data Standards non-functional requirements. No rate-limit headers
are returned. Use `updated-since` to poll incrementally rather than re-listing
the whole catalogue.

## What you cannot do here

Nothing about an identifiable customer. Usage, billing, accounts, service points
and DER data require ACCC accreditation as a CDR data recipient, mutual TLS, and
that customer's explicit consent. See
`skills/energy-queensland-consume-accredited-energy-data.md`.
