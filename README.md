# Moyasar (moyasar)

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
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Moyasar is a Saudi Arabian payment gateway that lets businesses accept online payments across mada, Visa, Mastercard, American Express, Apple Pay, Samsung Pay, and STC Pay. Its REST API (base `https://api.moyasar.com/v1`) covers payments (create, fetch, list, refund, capture, void), hosted invoices, card tokenization, webhooks, and payouts / disbursements.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/moyasar/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/moyasar/refs/heads/main/apis.yml)

## Access Model (Read This First)

- **Transport:** Request/response REST over HTTPS only. Plain HTTP is rejected. Base URL is `https://api.moyasar.com/v1`.
- **Authentication:** HTTP Basic auth. Your API **key is the username** and the **password is empty** — e.g. `curl https://api.moyasar.com/v1/payments -u sk_test_123:` (note the trailing colon).
- **Two key classes:**
  - **Publishable keys** (`pk_test_` / `pk_live_`) — safe for client-side use, restricted to creating payments and tokenizing cards, so raw card data never reaches your backend.
  - **Secret keys** (`sk_test_` / `sk_live_`) — authorize all account operations; keep them backend-only. If leaked, regenerate immediately.
- **Two modes:** `*_test_` keys drive a sandbox; `*_live_` keys move real money.
- **Amounts** are integers in the smallest currency unit — for SAR, halalas (`1.00 SAR = 100`).
- **Realtime updates** are delivered by **outbound webhooks over HTTP POST**, not a WebSocket. See the review note below.

## Tags

- Payments
- Payment Gateway
- Saudi Arabia
- MENA
- mada
- Cards
- Apple Pay
- STC Pay
- Invoices
- Fintech

## Timestamps

- **Created:** 2026-07-12
- **Modified:** 2026-07-12

## APIs

### Moyasar Payments API

Create, fetch, and list card / wallet payments and manage their lifecycle — refund, capture (for authorized payments), and void. Sources include `creditcard`, `token`, `applepay`, `samsungpay`, and `stcpay`.

- **Human URL:** [https://docs.moyasar.com/api/payments/01-create-payment](https://docs.moyasar.com/api/payments/01-create-payment)
- **Base URL:** `https://api.moyasar.com/v1`

#### Tags

- Payments
- Cards
- mada
- Refunds

#### Properties

- [Documentation](https://docs.moyasar.com/api/payments/01-create-payment)
- [API Reference](https://docs.moyasar.com/api/payments/02-fetch-payment)
- [OpenAPI](openapi/moyasar-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/moyasar.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/moyasar.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Moyasar Invoices API

Create hosted invoices that return a Moyasar-hosted checkout URL, then fetch, list, update, and cancel them. Supports bulk creation, expiry, and success / back / callback URLs.

- **Human URL:** [https://docs.moyasar.com/api/invoices/01-create-invoice](https://docs.moyasar.com/api/invoices/01-create-invoice)
- **Base URL:** `https://api.moyasar.com/v1`

#### Tags

- Invoices
- Hosted Checkout
- Billing

#### Properties

- [Documentation](https://docs.moyasar.com/api/invoices/01-create-invoice)
- [OpenAPI](openapi/moyasar-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/moyasar.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/moyasar.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Moyasar Tokens API

Tokenize mada / credit cards from the client side using a publishable key so card data never touches the merchant backend, then reuse the token as a payment source. Create and fetch tokens.

- **Human URL:** [https://docs.moyasar.com/api/other/tokens/create-token/](https://docs.moyasar.com/api/other/tokens/create-token/)
- **Base URL:** `https://api.moyasar.com/v1`

#### Tags

- Tokenization
- Cards
- Publishable Key

#### Properties

- [Documentation](https://docs.moyasar.com/api/other/tokens/create-token/)
- [API Reference](https://docs.moyasar.com/api/other/tokens/token-object/)
- [OpenAPI](openapi/moyasar-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/moyasar.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/moyasar.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Moyasar Webhooks API

Register HTTPS endpoints to receive server-to-server event notifications (`payment_paid`, `payment_failed`, `payment_refunded`, `payment_captured`, `payment_voided`, `payment_authorized`, and more). Create, list, fetch, and delete webhooks, list delivery attempts, and list available event types. Delivery is HTTP POST — there is no WebSocket surface.

- **Human URL:** [https://docs.moyasar.com/api/other/webhooks/webhook-reference/](https://docs.moyasar.com/api/other/webhooks/webhook-reference/)
- **Base URL:** `https://api.moyasar.com/v1`

#### Tags

- Webhooks
- Events
- Notifications

#### Properties

- [Documentation](https://docs.moyasar.com/api/other/webhooks/webhook-reference/)
- [API Reference](https://docs.moyasar.com/api/other/webhooks/create-webhook/)
- [OpenAPI](openapi/moyasar-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/moyasar.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/moyasar.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Moyasar Payouts API

Register payout accounts (bank or wallet) and send single, listed, or bulk payouts / disbursements. Create and list payout accounts, create single and bulk payouts, and fetch or list individual payouts.

- **Human URL:** [https://docs.moyasar.com/api/payouts/01-create-payout-account](https://docs.moyasar.com/api/payouts/01-create-payout-account)
- **Base URL:** `https://api.moyasar.com/v1`

#### Tags

- Payouts
- Disbursements
- Bank Transfer

#### Properties

- [Documentation](https://docs.moyasar.com/api/payouts/01-create-payout-account)
- [OpenAPI](openapi/moyasar-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/moyasar.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/moyasar.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

## Common Properties

- [Domain Security](security/moyasar-domain-security.yml)
- [Authentication](authentication/moyasar-authentication.yml)
- [LinkedIn](https://www.linkedin.com/company/moyasar)
- [Website](https://moyasar.com/)
- [Documentation](https://docs.moyasar.com/)
- [Plans](plans/moyasar-plans-pricing.yml)
- [Rate Limits](rate-limits/moyasar-rate-limits.yml)
- [Fin Ops](finops/moyasar-finops.yml)

## WebSocket Review

**Does Moyasar expose a documented public WebSocket API? No.** Moyasar's public API is request/response REST over HTTPS. Its only asynchronous surface is outbound webhooks delivered as HTTP POST to a merchant-registered endpoint (with retries and an optional shared secret) — not a `ws://` / `wss://` transport. No AsyncAPI document was authored. See [review.yml](review.yml).

## Real vs. Modeled

All endpoint **paths** in the OpenAPI and collections are grounded in the public Moyasar documentation. Request/response **JSON schemas** are a representative subset modeled from the docs (schemas allow additional properties); some field names and enum members were inferred rather than copied field-for-field. **Pricing** in `plans/` and `finops/` is modeled from public secondary sources (not an official Moyasar rate card) and is marked `reconciled: false`. Confirm exact rates and fields with Moyasar during reconciliation.

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
