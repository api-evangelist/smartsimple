# SmartSimple (smartsimple)

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
