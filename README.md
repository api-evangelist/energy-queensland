# Energy Queensland (energy-queensland)

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
