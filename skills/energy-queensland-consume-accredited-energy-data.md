---
name: Consume Ergon Energy Retail consumer energy data as an accredited CDR recipient
description: >-
  The full consented flow for an ACCC-accredited Consumer Data Right data
  recipient reading an Ergon Energy Retail customer's accounts, service points,
  interval usage, distributed energy resources, billing, invoices, balances,
  concessions and payment schedule. Includes the bulk-versus-specific-ids
  pattern, the AEMO secondary data holder caveat, and the exact scope each
  operation needs.
api: openapi/energy-queensland-cds-energy-openapi.yml
base_url: not publicly discoverable — published through the authenticated CDR Register
auth: FAPI 1.0 Advanced OAuth2 + OIDC over mutual TLS, per-consumer consent
operations:
  - getCustomer
  - getCustomerDetail
  - listEnergyAccounts
  - getEnergyAccountDetail
  - listElectricityServicePoints
  - getElectricityServicePointDetail
  - listElectricityUsageBulk
  - listElectricityUsageForServicePoints
  - getElectricityServicePointUsage
  - listElectricityDERBulk
  - getElectricityDERForServicePoint
  - listEnergyAccountBalancesBulk
  - getEnergyAccountBalance
  - listEnergyAccountBillingBulk
  - getBillingForEnergyAccount
  - listEnergyAccountInvoicesBulk
  - getEnergyAccountInvoices
  - getEnergyAccountConcessions
  - getEnergyAccountPaymentSchedule
generated: '2026-07-27'
method: generated
---

# Consume Ergon Energy Retail consumer energy data (accredited only)

**Read this first.** Nothing in this skill is callable without ACCC
accreditation. There is no sandbox published by Energy Queensland, no API key,
no partner tier and no commercial path. The gate is statutory. If you are not an
accredited CDR data recipient (or acting under the CDR representative or trusted
adviser pathways), stop here and use
`skills/energy-queensland-read-ergon-tariff-plans.md` instead.

Coverage limit worth knowing before you build: Ergon Energy Retail serves
**regional Queensland** only. South East Queensland is contestable and retailed
by third parties, so an Energex-area customer's data comes from AGL, Origin,
EnergyAustralia or whoever they buy from — not from Energy Queensland.

## Prerequisites

1. Accreditation with the ACCC (unrestricted or sponsored).
2. Client credentials plus transport and signing certificates from the CDR Register certificate authority.
3. Conformance Test Suite (CTS) testing completed.
4. Dynamic Client Registration with the data holder using a CDR Register software statement assertion.
5. A consent the individual customer approved, naming the scopes you need.

Resolve the data holder's InfoSec and resource base URIs through the
**authenticated** portion of the CDR Register — they are not public. Anonymous
`/.well-known/openid-configuration` on `public.cdr.ergonretail.com.au` returns
HTTP 404 by design. `api.cdr.ergonretail.com.au` demands a client certificate at
TLS handshake; that is the mTLS gate, not a fault.

## Required headers on every authenticated call

| Header | Notes |
|---|---|
| `x-v` | Mandatory. Endpoint version. |
| `x-min-v` | Optional lower bound for negotiation. |
| `x-fapi-interaction-id` | RFC 4122 UUID, played back in the response. |
| `x-fapi-auth-date` | Time the customer last authenticated. Customer-present calls. |
| `x-fapi-customer-ip-address` | Present for customer-present calls, **absent** for unattended calls — this is what distinguishes the two traffic classes for rate limiting and performance thresholds. |
| `x-cds-client-headers` | Base64 client headers. |

## Step 1 — identify the customer

`getCustomer` (`common:customer.basic:read`) then, if consented,
`getCustomerDetail` (`common:customer.detail:read`).

## Step 2 — enumerate accounts

`listEnergyAccounts` (`energy:accounts.basic:read`), filterable by
`open-status`. Each account carries `accountId` and `plans[]`, and each plan
carries `servicePointIds[]` — that array is the join to everything metered.

`getEnergyAccountDetail` (`energy:accounts.detail:read`) adds plan detail and
authorised contacts.

## Step 3 — pick bulk or specific

Every high-volume domain has a **bulk GET** and a **POST for specific ids**:

| Domain | Bulk | Specific ids | Scope |
|---|---|---|---|
| Balances | `listEnergyAccountBalancesBulk` | `listEnergyAccountBalancesSpecificAccounts` | `energy:billing:read` |
| Billing | `listEnergyAccountBillingBulk` | `listEnergyAccountBillingForSpecificAccounts` | `energy:billing:read` |
| Invoices | `listEnergyAccountInvoicesBulk` | `listEnergyInvoicesForSpecificAccounts` | `energy:billing:read` |
| Usage | `listElectricityUsageBulk` | `listElectricityUsageForServicePoints` | `energy:electricity.usage:read` |
| DER | `listElectricityDERBulk` | `listElectricityDERForSpecificServicePoints` | `energy:electricity.der:read` |

The POST variants create nothing — they exist only to carry an id list in a
body. There is no idempotency key anywhere on this surface, and none is needed.

Note the error-code shift: an unavailable or invalid id returns **404** when it
was supplied in the URI, and **422** when it was supplied in the request body
(`urn:au-cds:error:cds-energy:Authorisation/UnavailableEnergyAccount` /
`InvalidEnergyAccount`, and the ServicePoint equivalents).

## Step 4 — metered data

- `listElectricityServicePoints` (`energy:electricity.servicepoints.basic:read`) and `getElectricityServicePointDetail` (`...detail:read`) — NMI, jurisdiction, classification, status, meters, registers, distribution loss factor, related market participants.
- `getElectricityServicePointUsage` / `listElectricityUsageBulk` with `interval-reads`, `oldest-date`, `newest-date` — basic or interval reads.
- `getElectricityDERForServicePoint` / `listElectricityDERBulk` — approved capacity, phases, AC connections, DER devices, protection mode, islandable installation.

**Shared Responsibility caveat:** service point, usage and DER data originate
with **AEMO** as the CDR secondary data holder, not with Ergon. When AEMO is
unavailable these calls fail without breaching Ergon's own availability
obligation, and the error payload uses `PrimaryErrorV1`, which sets
`isSecondaryDataHolderError: true`. Handle that flag explicitly — it tells you
to retry rather than to treat the consent as broken.

## Step 5 — money

`getEnergyAccountBalance`, `getBillingForEnergyAccount` (usage, demand, once-off,
other-charge and payment transaction types), `getEnergyAccountInvoices`,
`getEnergyAccountConcessions` (`energy:accounts.concessions:read`) and
`getEnergyAccountPaymentSchedule` (`energy:accounts.paymentschedule:read`).

Billing, invoice and usage operations take date ranges — an unparseable date
returns `400 urn:au-cds:error:cds-all:Field/InvalidDateTime`.

## Pagination, throttling and identifiers

- `page` / `page-size` (default 25, max 1000), with `meta.totalRecords`, `meta.totalPages` and `links`.
- Customer-present: 10 TPS per customer, 50 TPS per software product, unlimited sessions. Unattended: 20 sessions per day per customer per software product, 100 calls per session, 5 TPS per session. See `rate-limits/energy-queensland-rate-limits.yml`.
- `accountId` and `servicePointId` are **consent-scoped tokenised** values. They differ per data recipient and do not survive consent revocation — never persist them as durable cross-system keys.

## Before you start a run

Poll `getStatus` and `getOutages` on
`https://public.cdr.ergonretail.com.au/cds-au/v1` — anonymous, cheap, and the
contractual availability signal. See
`skills/energy-queensland-check-cdr-availability.md`.
