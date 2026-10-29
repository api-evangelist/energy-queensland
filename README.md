# Energy Queensland

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

Energy Queensland Limited is the Queensland Government-owned corporation formed on 30 June 2016 by merging Ergon Energy and Energex. It is the whole Queensland electricity value chain below transmission in a single holding company: Energex distributes to roughly 1.5 million connections across South East Queensland, Ergon Energy Network distributes across regional Queensland, Ergon Energy Retail is the notified-price retailer for about 760,000 regional customers, Yurika sells energy services and telecommunications, and SPARQ Solutions provides group ICT. That dual role is what makes its API posture worth recording precisely, because the two halves of the business sit on opposite sides of a statutory line. The RETAIL half is a designated Consumer Data Right energy data holder and its implementation is verified live, not claimed: "Ergon Energy Retail" (ABN 11121177802) is listed on the ACCC CDR Register with publicBaseUri https://public.cdr.ergonretail.com.au and productBaseUri https://cdr.energymadeeasy.gov.au/ergon, both of which answered HTTP 200 to anonymous, standards-conformant calls on 2026-07-27, returning 36 REGULATED electricity plans and a CDS discovery status of OK. The DISTRIBUTION half - the poles and wires - is not a CDR data holder at all, publishes no developer portal, no open-data API and no machine-readable contract, and has no developer., developers., api., docs. or data. subdomain in DNS on energyq.com.au, ergon.com.au or energex.com.au. Its network data reaches the public as PDF and XLSX planning reports, registration-free but non-programmatic map viewers, and exactly one open-licensed spatial dataset deposited on the Queensland Government's CKAN portal. The split is the finding: a mandate transplanted from banking produced a real, anonymous, standardised API on the regulated retail side and changed nothing whatsoever on the network side it never touched.

**Areas:** Energy · Australia · Utilities · Electricity · Grid · Distribution Network · Energy Retail · Consumer Data Right · CDR · Product Reference Data · Queensland · Smart Metering

## Energy Queensland on APIs.io

Everything profiled for Energy Queensland is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/energy-queensland/](https://apis.io/providers/energy-queensland/)** — or go straight to one of the APIs or properties below.

### APIs (9)

- [Energy Queensland Data Holder Customers API](https://apis.io/apis/energy-queensland/energy-queensland-data-holder-customers-api/) — Data Holder Customer endpoints
- [Energy Queensland Data Holder Operations API](https://apis.io/apis/energy-queensland/energy-queensland-data-holder-operations-api/) — Data Holder Operations endpoints
- [Energy Queensland Distributed Energy Resources API](https://apis.io/apis/energy-queensland/energy-queensland-distributed-energy-resources-api/) — Distributed Energy Resource endpoints
- [Energy Queensland Electricity Service Points API](https://apis.io/apis/energy-queensland/energy-queensland-electricity-service-points-api/) — Electricity Service Point endpoints
- [Energy Queensland Electricity Usage API](https://apis.io/apis/energy-queensland/energy-queensland-electricity-usage-api/) — Electricity Usage endpoints
- [Energy Queensland Energy Account Balances API](https://apis.io/apis/energy-queensland/energy-queensland-energy-account-balances-api/) — Energy Account Balance endpoints
- [Energy Queensland Energy Account Billing API](https://apis.io/apis/energy-queensland/energy-queensland-energy-account-billing-api/) — Energy Account Billing endpoints
- [Energy Queensland Energy Accounts API](https://apis.io/apis/energy-queensland/energy-queensland-energy-accounts-api/) — Energy Account endpoints
- [Energy Queensland Energy Plans API](https://apis.io/apis/energy-queensland/energy-queensland-energy-plans-api/) — Energy Plan endpoints

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [energy-queensland](https://apis.io/servers/energy-queensland/energy-queensland/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Energy Queensland Agentic Access](https://apis.io/agentic-access/energy-queensland/energy-queensland-agentic-access/)

#### Collections (2)

Postman and Open Collection request collections.

- [CDR Common API](https://apis.io/collections/energy-queensland/open-energy-queensland-cds-common/)
- [CDR Energy API](https://apis.io/collections/energy-queensland/open-energy-queensland-cds-energy/)

#### Overlays (2)

OpenAPI overlays, including conversational phrasing for each operation.

- [Energy Queensland Cds Common Overlay](https://apis.io/overlays/energy-queensland/energy-queensland-cds-common-overlay/)
- [Energy Queensland Cds Energy Overlay](https://apis.io/overlays/energy-queensland/energy-queensland-cds-energy-overlay/)

#### Security (2)

Authentication, trust centre, and vulnerability disclosure.

- [Energy Queensland Authentication](https://apis.io/security/energy-queensland/energy-queensland-authentication/)
- [Energy Queensland Domain Security](https://apis.io/security/energy-queensland/energy-queensland-domain-security/)

#### OAuth scopes (1)

The permissions the API asks for.

- [Energy Queensland Scopes](https://apis.io/scopes/energy-queensland/energy-queensland-scopes/)

#### Rate limits (1)

Published request limits.

- [Energy Queensland Rate Limits](https://apis.io/rate-limits/energy-queensland/energy-queensland-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://www.energyq.com.au/)
- [Documentation](https://consumerdatastandardsaustralia.github.io/standards/)
- [API reference](https://consumerdatastandardsaustralia.github.io/standards/#energy-apis)
- [GitHub](https://github.com/Energy-Queensland)
- [Status](https://public.cdr.ergonretail.com.au/cds-au/v1/discovery/status)

## API Evangelist rating

**Kin Score 38.6** — thin · rubric 0.24.0 · scored 2026-10-17

| Facet | Score |
|---|---|
| Discoverability | 66.1 |
| Contract quality | 45.9 |
| Contract governance | 18.2 |
| Operational transparency | 65.8 |
| Developer ergonomics | 30.4 |
| Access clarity | 7.9 |

**Agent readiness 26.4** — agent-aware

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | — |
| MCP Server | — |
| Auth Clarity | bearer (partial credit) |
| Idempotency | — |
| Error Semantics | verified |
| OpenAPI Examples | — |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | — |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |

**Regulatory alignment 32.0** — Energy & Utilities

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/energy-queensland/](https://apis.io/providers/energy-queensland/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Energy Queensland: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/energy-queensland/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
