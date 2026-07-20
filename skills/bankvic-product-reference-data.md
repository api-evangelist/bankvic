---
name: Query BankVic product reference data
description: >-
  Retrieve BankVic's public product catalogue (accounts, loans, term deposits, credit
  cards) and full product detail via the unauthenticated CDR Product Reference Data API.
api: openapi/bankvic-cds-banking-products-openapi.yml
operations:
  - listBankingProducts
  - getBankingProductDetail
---

# Query BankVic product reference data

BankVic exposes a **public, unauthenticated** Consumer Data Right (CDR) Product
Reference Data API. No API key, OAuth token, or mTLS is required — only the mandatory
`x-v` version header. Base URL: `https://ib.bankvic.com.au/openbanking/cds-au/v1`.

## Rules that always apply
- Send the header **`x-v: 4`** on every request. Omitting it returns `400`
  (`urn:au-cds:error:cds-all:Header/Missing`); an unsupported version returns `406`
  (`urn:au-cds:error:cds-all:Header/InvalidVersion`). Confirmed live: `x-v:3` → 406,
  `x-v:4` → 200.
- Responses are JSON with a `data` object plus `meta` (`totalRecords`, `totalPages`)
  and `links` (`self`, `first`, `prev`, `next`, `last`).
- Errors use the CDR envelope `{ "errors": [ { "code", "title", "detail",
  "meta": { "urn" } } ] }` — see `errors/bankvic-problem-types.yml`.

## Step 1 — List products (`listBankingProducts`)
`GET /banking/products` with header `x-v: 4`.

Useful query params: `page` (1-based), `page-size` (default 25),
`product-category` (e.g. `TERM_DEPOSITS`, `TRANS_AND_SAVINGS_ACCOUNTS`,
`RESIDENTIAL_MORTGAGES`, `CRED_AND_CHRG_CARDS`), `effective` (`CURRENT|FUTURE|ALL`),
`updated-since` (DateTimeString), `brand`.

Read `data.products[]` for `productId`, `name`, `productCategory`, `description`,
`applicationUri`. Follow `links.next` to page through the full set (~55 products).

## Step 2 — Get product detail (`getBankingProductDetail`)
For a `productId` from Step 1: `GET /banking/products/{productId}` with header `x-v: 4`.

The `data` object extends the summary with `features`, `constraints`, `eligibility`,
`fees` (with nested `discounts`), `depositRates` / `lendingRates` (with `tiers`),
`bundles`, and `cardArt`. An unknown `productId` returns `404`
(`urn:au-cds:error:cds-all:Resource/NotFound`).

## Notes
- This API is **read-only**; there is no mutation and no idempotency key.
- Consented account, balance, transaction, direct-debit, scheduled-payment, and payee
  data is **not** reachable here — it is shared only through an accredited CDR Data
  Recipient under the FAPI 2.0 security profile (see `authentication/bankvic-authentication.yml`).
