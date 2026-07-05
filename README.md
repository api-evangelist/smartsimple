# SmartSimple (smartsimple)

SmartSimple Software builds **SmartSimple Cloud**, a configurable cloud platform for grants management, research and government funding administration, corporate social responsibility (CSR), scholarships, and case management. Founded in 2002 and headquartered in Toronto, SmartSimple serves 500+ clients across 192 countries (and merged with Foundant Technologies in 2024).

The platform exposes three documented programmatic interfaces on each client instance:

- **SmartConnect** — a JSON-based RESTful API (the current, fully supported API)
- **OData** — a reporting service (V2/V3/V4)
- **Web Services** — a legacy SOAP API

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/smartsimple/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/smartsimple/refs/heads/main/apis.yml)

## Access Model — Instance-Scoped and Gated

SmartSimple has a **real, documented API**, but it is **not a single public gateway**. Every customer runs on their own tenant (`{alias}.smartsimple.com`), and the APIs are enabled and called against that instance. The documentation is public (`wiki.smartsimple.com`, `supporthub.smartsimple.com`), but making calls requires a provisioned SmartSimple subscription plus:

- an **API user account** (username, password, `companyid`, `alias`), or a **Bearer user access token**, and
- a per-function **encrypted `apitoken`** for SmartConnect functions.

Because the base URL is per-instance and no anonymous public endpoint exists, the endpoints in this catalog are **modeled** (`endpointsModeled: true`) against the documented per-instance API surface rather than confirmed against a live public base URL. No OpenAPI or Postman collection is published here, because there is no single testable public base URL.

## APIs

All SmartConnect calls POST to `https://{alias}.smartsimple.com/API/{version}/{recordtype}/` (APIVersion 2 standardized the syntax as of the August 2022 upgrade). Standard fields use `sf_` prefixes and custom fields use `cf_` (by name or ID).

### SmartSimple SmartConnect Records API
Get, list, and update (create) records in SmartSimple's Universal Tracking Application (UTA) at Level 1, Level 2, and Level 3 — the grant applications, reviews, and sub-records at the heart of the platform. Endpoints: `/API/1/levelone/`, `/API/1/leveltwo/`, `/API/1/levelthree/`.

### SmartSimple SmartConnect Users API
Get, list, and update people (applicants, reviewers, contacts, staff) and their standard/custom fields and addresses via `/API/1/user/`.

### SmartSimple SmartConnect Organizations API
Get, list, and update organizations (companies, grantee institutions, accounts) via `/API/1/company/`.

### SmartSimple SmartConnect Transactions API
Get, list, and update UTA transaction records (payments, disbursements, budget lines) via `/API/1/transactions/`, with criteria filtering, sorting, and pagination.

### SmartSimple SmartConnect Files API
Download a single file, list files on a record or field, and keyword-search files using the Download File, List Files, and Search Files actions.

### SmartSimple OData Reporting API
Consume report data over OData V2/V3/V4, with `pub` (public) and `pri` (basic-auth) endpoints — e.g. `/OData/V4/pri/{reportid}/Service.svc/`. Reports are currently the only entities exposed over OData.

### SmartSimple Web Services (SOAP) API
The legacy SOAP interface, exposed per instance via a WSDL at `/WS/services/UtaUpdate?wsdl` (e.g. `https://smart.smartsimple.biz/WS/services/UtaUpdate?wsdl`). Superseded by SmartConnect but still documented and supported.

## SmartConnect Actions

`Get`, `List`, `Update` (recordid `0` creates), `Get Meta` / `Update Meta`, `Download File` / `List Files` / `Search Files`, `List Associations` / `Update Associations`, `List Multiple Addresses` / `Update Multiple Addresses`, and `Variables Replace`.

## Rate Limits

- Roughly **1,000 SmartConnect API calls per instance per hour**.
- A single `List` call returns at most **10,000 records**; larger sets require pagination (`recordsperpage`, `recordstart`, `pagenum`).
- SmartConnect is documented as **not intended for high-volume bulk export/import**.

See [rate-limits/smartsimple-rate-limits.yml](rate-limits/smartsimple-rate-limits.yml).

## Pricing

Contact-sales enterprise SaaS. Third-party listings put the entry point around **6,000 USD/year** (~500 USD/month), with the annual fee scaled by internal users, monthly usage hours, external users, hosting model (multi-tenant / single-tenant / on-premise), and add-ons (High Performance Private Cloud, AI features). The APIs are included with the subscription rather than billed per call. See [plans/smartsimple-plans-pricing.yml](plans/smartsimple-plans-pricing.yml) and [finops/smartsimple-finops.yml](finops/smartsimple-finops.yml).

## WebSocket Review

SmartSimple does **not** expose a documented public WebSocket API. All documented surfaces (SmartConnect REST, OData, SOAP) are request/response over HTTPS. See [review.yml](review.yml).

## Common Properties

- [Website](https://www.smartsimple.com)
- [LinkedIn](https://www.linkedin.com/company/smartsimple-software-inc)
- [Documentation](https://wiki.smartsimple.com/wiki/APIs)
- [Interactive Demo](https://api.smartsimple.com/devtools/api.html)
- [Pricing](https://www.smartsimple.com/pricing)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
