# Smartrr (smartrr)

Smartrr is a subscription and loyalty platform for Shopify DTC brands. It layers subscribe-and-save subscriptions, a branded customer account portal, loyalty and rewards, referrals, bundles, and retention tooling on top of Shopify. Smartrr exposes a real, documented **Vendor API** at `https://api.smartrr.com` that lets merchants programmatically manage the subscriptions their customers hold - modeled as "purchase states" - along with subscribers, orders, bills, and the selling plans / subscription programs products are sold on.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/smartrr/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/smartrr/refs/heads/main/apis.yml)

## Access Model

The Smartrr API is a **commercial, account-gated API** - not open source, and not open-signup. A few honest notes on how access works:

- **You need a Smartrr account.** Smartrr is a paid Shopify subscription app (Launch, Grow, Excel tiers, plus enterprise). The Vendor API is included with a subscription; there is no separate per-call API fee.
- **Authentication is a per-organization API access token.** You generate it in the Smartrr admin under the **Integrations** tab ("Add Key") and send it on every request in the `x-smartrr-access-token` header (`apiKey` scheme).
- **The specification itself is public.** Smartrr serves a full OpenAPI 3.0 document (116 operations) unauthenticated at [`https://api.smartrr.com/docs/spec.json`](https://api.smartrr.com/docs/spec.json), rendered with Redoc at [`https://api.smartrr.com/docs/redoc/`](https://api.smartrr.com/docs/redoc/). So the endpoint catalog is openly documented even though calling it requires an account token.
- **It sits on top of Shopify.** Many resources (customers, orders, selling plans) mirror or derive from the underlying Shopify store.

The `openapi/smartrr-openapi.yml` in this repo is a **curated subset** of Smartrr's live specification covering the core Subscriptions, Subscribers, Orders, Bills, Plans, and Webhooks resources. Endpoint paths and methods are taken directly from the live spec (confirmed, not modeled); request/response bodies are summarized.

## Tags

- Subscriptions
- Loyalty
- Shopify
- Ecommerce
- DTC
- Recurring Revenue
- Subscription Management

## Timestamps

- **Created:** 2026-07-10
- **Modified:** 2026-07-10

## APIs

### Smartrr Subscriptions API

Read and manage the subscriptions customers hold, which Smartrr models as "purchase states". Create subscriptions, list them by organization, customer, or Shopify subscription ID, and drive the full lifecycle - skip, unskip, pause, activate, cancel, set the next billing date, change the selling plan, add or swap line items, and run bulk operations.

- **Human URL:** [https://api.smartrr.com/docs/redoc/](https://api.smartrr.com/docs/redoc/)
- **Base URL:** `https://api.smartrr.com`

### Smartrr Subscribers API

Work with subscribers, which Smartrr models as customer relationships. List and retrieve customers by Smartrr or Shopify ID, read their payment methods and orders, import customers and payment methods from Shopify, fetch a referral code and link, and add loyalty points.

- **Human URL:** [https://api.smartrr.com/docs/redoc/](https://api.smartrr.com/docs/redoc/)
- **Base URL:** `https://api.smartrr.com`

### Smartrr Orders and Bills API

List and retrieve the orders subscriptions generate, open and close orders, and manage the recurring bills (subscription transactions) behind them - read bills, inspect a bill's audit history, and retry or cancel bills individually or in bulk.

- **Human URL:** [https://api.smartrr.com/docs/redoc/](https://api.smartrr.com/docs/redoc/)
- **Base URL:** `https://api.smartrr.com`

### Smartrr Plans and Purchasables API

Read the products and terms subscriptions are sold on - purchasables and purchasable collections, selling plans and selling plan groups, and the subscription programs configured for a shop. Update purchasables to control what is available for subscription.

- **Human URL:** [https://api.smartrr.com/docs/redoc/](https://api.smartrr.com/docs/redoc/)
- **Base URL:** `https://api.smartrr.com`

### Smartrr Webhooks API

Register HTTP endpoints to receive Smartrr event notifications. Create, list, edit, and delete webhooks for the organization so external systems can react to subscription and billing events in near real time.

- **Human URL:** [https://help.smartrr.com/docs/support/integrations/webhooks](https://help.smartrr.com/docs/support/integrations/webhooks)
- **Base URL:** `https://api.smartrr.com`

## Authentication

All requests are authenticated with a per-organization API access token sent in the `x-smartrr-access-token` header. Generate a token in the Smartrr admin under **Integrations → Add Key**.

## Pricing

Smartrr is billed as a Shopify subscription app: a fixed monthly base fee tied to a plan tier plus a usage fee of **1% of subscriber GMV** (with a no-transaction-fee guarantee - no extra per-order fee).

- **Launch** - $99/mo + 1% subscriber GMV
- **Grow** - $299/mo + 1% subscriber GMV
- **Excel** - from $499/mo + 1% subscriber GMV
- **Enterprise / Custom** - negotiated flat-fee annual contracts with volume discounts

A 14-day free trial is offered; contracts are month-to-month. See [`plans/smartrr-plans-pricing.yml`](plans/smartrr-plans-pricing.yml) and [https://smartrr.com/pricing](https://smartrr.com/pricing).

## Real-Time / WebSocket

Smartrr does **not** expose a documented public WebSocket API. The Vendor API is request/response REST over HTTPS; the only server-push mechanism is outbound webhooks. See [`review.yml`](review.yml).

## Common Properties

- [Website](https://smartrr.com)
- [LinkedIn](https://www.linkedin.com/company/smartrr)
- [Documentation](https://help.smartrr.com/docs)
- [API Reference](https://api.smartrr.com/docs/redoc/)
- [Plans](plans/smartrr-plans-pricing.yml)
- [Rate Limits](rate-limits/smartrr-rate-limits.yml)
- [Fin Ops](finops/smartrr-finops.yml)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
