# Moyasar (moyasar)

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
