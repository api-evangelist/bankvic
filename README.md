# BankVic (bankvic)

BankVic is an Australian customer-owned mutual bank and the trading name of Police Financial Services Limited, an authorised deposit-taking institution (ADI) founded in 1974 and headquartered in Melbourne, Victoria. Member-owned rather than shareholder-driven, it has served Victoria's police, health, and emergency-services communities and the broader Victorian public under a "people before profits" ethos for more than fifty years. As a regulated ADI it participates in Australia's Consumer Data Right (CDR / Open Banking) regime and publishes a public, unauthenticated Product Reference Data (PRD) API.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/bankvic/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/bankvic/refs/heads/main/apis.yml)

## Tags

- Financial
- Banks
- Open Banking
- CDR
- Consumer Banking
- Australia
- Mutual Bank
- Product Reference Data

## Timestamps

- **Created:** 2026-07-20
- **Modified:** 2026-07-20

## APIs

### BankVic CDR Product Reference Data API

Public, unauthenticated Consumer Data Right Product Reference Data (PRD) API exposing BankVic's product catalogue (accounts, loans, term deposits, credit cards) with terms, conditions, and key features. Live at the standard CDS path `GET /banking/products` and `GET /banking/products/{productId}`; confirmed returning HTTP 200 with `x-v: 4` and a `data.products` array (55 products across 11 pages). The contract conforms to the shared DSB Consumer Data Standards, not a bank-proprietary specification.

- **Human URL:** [https://www.bankvic.com.au/get-help/open-banking/](https://www.bankvic.com.au/get-help/open-banking/)
- **Base URL:** `https://ib.bankvic.com.au/openbanking/cds-au/v1`

#### Tags

- CDR
- Open Banking
- Product Reference Data
- Banking
- Australia

#### Properties

- [Documentation](https://www.bankvic.com.au/get-help/open-banking/)
- [API Reference](https://consumerdatastandardsaustralia.github.io/standards/#cdr-banking-api_get-products)
- [OpenAPI](openapi/bankvic-cds-banking-products-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)

## Common Properties

- [Website](https://www.bankvic.com.au/)
- [Documentation](https://www.bankvic.com.au/get-help/open-banking/)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
