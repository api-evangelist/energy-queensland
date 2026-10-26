# Energy Queensland (energy-queensland)

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

Energy Queensland Limited is the Queensland Government-owned corporation formed on 30 June 2016 by merging Ergon Energy and Energex. It is the whole Queensland electricity value chain below transmission in a single holding company: Energex distributes to roughly 1.5 million connections across South East Queensland, Ergon Energy Network distributes across regional Queensland, Ergon Energy Retail is the notified-price retailer for about 760,000 regional customers, Yurika sells energy services and telecommunications, and SPARQ Solutions provides group ICT. That dual role is what makes its API posture worth recording precisely, because the two halves of the business sit on opposite sides of a statutory line. The **retail** half is a designated Consumer Data Right energy data holder and its implementation is verified live, not claimed: "Ergon Energy Retail" (ABN 11121177802) is listed on the ACCC CDR Register with `publicBaseUri https://public.cdr.ergonretail.com.au` and `productBaseUri https://cdr.energymadeeasy.gov.au/ergon`, both of which answered HTTP 200 to anonymous, standards-conformant calls on 2026-07-27, returning 36 REGULATED electricity plans and a CDS discovery status of OK. The **distribution** half — the poles and wires — is not a CDR data holder at all, publishes no developer portal, no open-data API and no machine-readable contract, and has no `developer.`, `developers.`, `api.`, `docs.` or `data.` subdomain in DNS on energyq.com.au, ergon.com.au or energex.com.au. Its network data reaches the public as PDF and XLSX planning reports, registration-free but non-programmatic map viewers, and exactly one open-licensed spatial dataset deposited on the Queensland Government's CKAN portal.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/energy-queensland/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/energy-queensland/refs/heads/main/apis.yml)

## Tags

- Energy
- Australia
- Utilities
- Electricity
- Grid
- Distribution Network
- Energy Retail
- Consumer Data Right
- CDR
- Product Reference Data
- Queensland
- Smart Metering
- Solar
- DER
- Open Data

## Timestamps

- **Created:** 2026-07-27
- **Modified:** 2026-07-27

## Mandate

| | |
|---|---|
| **Home market** | Australia |
| **Tier** | Network distributor (Energex + Ergon Energy Network) that also owns a mandated retailer (Ergon Energy Retail) |
| **Mandate regime** | Consumer Data Right (energy) — Part IVD, Competition and Consumer Act 2010; ACCC as regulator, Treasury Data Standards Body as spec author. Binds the **retailer**; distributors are not designated. |
| **Mandate status** | **Live and implemented** — verified via CDR Register entry, a live standards-conformant host on an Energy Queensland domain, and 36 live branded plans on the AER's host |
| **Data standard** | CDR Consumer Data Standards (energy) — CDR Energy API v1.36.0 + CDR Common API v1.36.0, OpenAPI 3.0.3, `x-v` header versioning. No Green Button / ESPI, OCPP/OCPI, OpenADR, IEEE 2030.5 or IEC CIM reference found. |
| **Consumer data API** | Yes — accredited CDR data recipients only, with consumer consent, over mTLS |
| **Open market data** | No — no open-data portal, no grid/network API; one open-licensed GIS dataset sits on the state's CKAN portal |
| **Access gate** | Accredited-only for consumer data; no gate at all on product reference data; no API of any kind on the network side |
| **Developer portal** | None — no developer/api/docs/data subdomain resolves on any group domain |

Energy Queensland is the sharpest single-company test of whether a statutory data mandate is what produces an API, because it contains the mandated case and the control case inside one balance sheet. The regulated retail subsidiary is a live, register-listed, standards-conformant API publisher. The 2.3-million-connection distribution business the mandate never touched publishes nothing programmable. Nothing about engineering capability, data volume, customer count or ownership differs between the two halves — the only variable is whether Part IVD applied.

Designation did not equal implementation even here: the ACCC granted Ergon Energy Queensland a section 56GD exemption on 25 August 2023 deferring certain CDR obligations for non-complex and complex requests until 1 July 2024.

## APIs

### Ergon Energy Retail CDR Energy Product Reference Data API

The unauthenticated Consumer Data Right Product Reference Data surface for Energy Queensland's retail brand — Get Generic Plans and Get Generic Plan Detail from the Consumer Data Standards CDR Energy API. In CDR energy, unlike CDR banking, generic plan data is not served by the data holder's own host: it is served centrally by the Australian Energy Regulator's Energy Made Easy CDR host under a per-brand path. Confirmed live 2026-07-27: `GET /cds-au/v1/energy/plans` with `x-v: 1` returned HTTP 200 and `meta.totalRecords 36`; the first record is `planId ERG1064038RRE1@EME`, brand `ergon`, `type REGULATED`. Plan detail requires `x-v: 3` (HTTP 406 at `x-v: 1`). No key, no signup, no accreditation.

- **Human URL:** [https://consumerdatastandardsaustralia.github.io/standards/#energy-apis](https://consumerdatastandardsaustralia.github.io/standards/#energy-apis)
- **Base URL:** `https://cdr.energymadeeasy.gov.au/ergon/cds-au/v1`

#### Tags

- Energy Plans
- Product Reference Data
- Consumer Data Right
- Tariffs
- Regulated Prices
- Australia

#### Properties

- [OpenAPI](openapi/energy-queensland-cds-energy-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [API Reference](https://consumerdatastandardsaustralia.github.io/standards/#energy-apis)
- [API Reference](https://consumerdatastandardsaustralia.github.io/standards/#get-generic-plans)
- [API Reference](https://consumerdatastandardsaustralia.github.io/standards/#get-generic-plan-detail)
- [Documentation](https://consumerdatastandardsaustralia.github.io/standards/)
- [Registry](https://api.cdr.gov.au/cdr-register/v1/energy/data-holders/brands/summary)

### Ergon Energy Retail CDR Discovery API

Ergon Energy Retail's own registered Consumer Data Right public base URI, serving the two unauthenticated Data Holder Operations endpoints of the Consumer Data Standards CDR Common API — Get Status and Get Outages. This is the only anonymously callable API surface hosted on an Energy Queensland controlled domain. Confirmed live 2026-07-27 (HTTP 200 with `x-v: 1`, status OK, empty outages array). The base URI serves nothing else anonymously — `/cds-au/v1/energy/plans`, the site root and `/.well-known/openid-configuration` all return an nginx HTTP 404.

- **Human URL:** [https://consumerdatastandardsaustralia.github.io/standards/#common-apis](https://consumerdatastandardsaustralia.github.io/standards/#common-apis)
- **Base URL:** `https://public.cdr.ergonretail.com.au/cds-au/v1`

#### Tags

- Discovery
- Status
- Outages
- Consumer Data Right
- Australia

#### Properties

- [OpenAPI](openapi/energy-queensland-cds-common-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [API Reference](https://consumerdatastandardsaustralia.github.io/standards/#get-status)
- [API Reference](https://consumerdatastandardsaustralia.github.io/standards/#get-outages)
- [Status](https://public.cdr.ergonretail.com.au/cds-au/v1/discovery/status)
- [Documentation](https://consumerdatastandardsaustralia.github.io/standards/)

### Ergon Energy Retail CDR Energy Consumer Data API

The consumer-authorised half of the Consumer Data Right energy obligation — electricity service points, usage, distributed energy resources, energy accounts, balances, invoices, billing, concessions and payment schedules, sixteen paths in all. Real and mandated, but not open: reachable only by an ACCC-accredited CDR data recipient over mutual TLS with FAPI-profile OAuth2/OIDC after the individual customer consents. No base URL is recorded because none is publicly discoverable and no endpoint was called. The host `api.cdr.ergonretail.com.au` does resolve and its TLS handshake emits a Request CERT message backed by a private certificate chain — the mTLS gate, observed directly.

- **Human URL:** [https://consumerdatastandardsaustralia.github.io/standards/#energy-apis](https://consumerdatastandardsaustralia.github.io/standards/#energy-apis)

#### Tags

- Energy Accounts
- Electricity Usage
- Billing
- Distributed Energy Resources
- Consumer Data Right
- Australia

#### Properties

- [OpenAPI](openapi/energy-queensland-cds-energy-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [API Reference](https://consumerdatastandardsaustralia.github.io/standards/#energy-apis)
- [Authentication](https://consumerdatastandardsaustralia.github.io/standards/#security-profile)
- [Documentation](https://consumerdatastandardsaustralia.github.io/standards/)

## Common Properties

- [Website](https://www.energyq.com.au/)
- [GitHub Organization](https://github.com/Energy-Queensland)
- [LinkedIn](https://au.linkedin.com/company/energyq)
- [Status](https://public.cdr.ergonretail.com.au/cds-au/v1/discovery/status)
- [Registry](https://api.cdr.gov.au/cdr-register/v1/energy/data-holders/brands/summary)
- [Documentation](https://consumerdatastandardsaustralia.github.io/standards/)
- [Data](https://www.data.qld.gov.au/dataset/ergon-energy-electrical-distribution-network-series)
- [Regulatory](https://www.accc.gov.au/public-registers/exemption-for-ergon-energy-queensland-pty-ltd)

## Maintainers

- **Kin Lane** — kin@apievangelist.com
