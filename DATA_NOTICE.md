# Data Notice

## Purpose

This repository is a technical sample for the [DACH Package Holiday Price API Actor](https://apify.com/kamerozkan/dach-package-holiday-price-api). It demonstrates one exact public Example Task input, two exact release-QA inputs, and privacy-minimized output projections.

It is not a booking service, a continuous real-time feed, a complete travel market, or a price guarantee.

## Audit snapshot

The following state was verified through the Apify API, public Store page, and authenticated owner console on 2026-07-28:

| Item | Verified value |
|---|---|
| Actor | `kamerozkan/dach-package-holiday-price-api` |
| Actor ID | `wgrg8RIdKtTl3x5UT` |
| Public | `true` |
| Current latest build | `1.0.17`, build ID `feNolI1qjKuod6aia`, status `SUCCEEDED` |
| Public Store Example Tasks | 1 |
| Public Example Task | `XzYQCBdhxElKX9CMM`, `Compare package holidays from Berlin`, 23 runs |
| Latest successful public task run | `QkVcaNfb3ChTziVgN`, build `1.0.14` |
| Public task dataset | `ozxjz9utd0IHgwj9l`, 5 records |

The inspected public task run used build `1.0.14`. The current `1.0.17` build completed successfully after that run, so this repository does not claim runtime validation of `1.0.17`.

## Input provenance

- [`01_public_berlin_example_input.json`](01_public_berlin_example_input.json) is the exact input exposed by the sole public Store Example Task.
- [`02_live_offer_qa_input.json`](02_live_offer_qa_input.json) is the exact fixed-date input from a live-source release-QA run completed on 2026-07-26. It is historical replay material, not a second public Store example.
- [`03_comparison_forecast_qa_input.json`](03_comparison_forecast_qa_input.json) is the exact fixed-date input from a separate live-source feature-QA run completed on 2026-07-26. It is historical replay material, not a public Store example.

Fixed dates can expire. For a new run, replace them with valid absolute dates or rolling values such as `8 weeks` and `10 weeks`.

## Output provenance

### Output 01

[`01_public_task_offer_projection.json`](01_public_task_offer_projection.json) is a field-level projection of the first row in dataset `ozxjz9utd0IHgwj9l`, produced by successful public task run `QkVcaNfb3ChTziVgN`.

The five-row dataset contained one offer row for each selected source: TUI, DERTOUR, weg.de, ab-in-den-urlaub.de, and alltours. Output 01 preserves only fields directly inspected in the owner console. No omitted values were inferred or recreated.

### Outputs 02 and 03

[`02_live_comparison_projection.json`](02_live_comparison_projection.json) and [`03_live_insufficient_forecast.json`](03_live_insufficient_forecast.json) are privacy-minimized projections from the 2026-07-26 local release-QA dataset that used live source responses. They are not claimed to come from the public task dataset.

Output 03 intentionally preserves `recommendation = insufficient_data`, low confidence, the evidence count, rationale, and disclaimer. It shows that the Actor can abstain instead of presenting a forecast without enough observations.

## Redactions and omissions

The samples omit or replace:

- opaque offer, comparison, series, and forecast keys
- operator offer identifiers
- image arrays
- exact latitude and longitude
- full source URLs with long query strings
- raw source payloads
- request metadata, IP information, user-agent information, cookies, and signatures

Public hotel names, GIATA identifiers, operators, dates, airports, prices, observation times, and decision fields were retained where needed to explain the contract. No customer or traveller identity data is included.

## Source and affiliation boundary

The Actor is an independent, unofficial tool. It is not affiliated with, endorsed by, or sponsored by TUI, DERTOUR, weg.de, ab-in-den-urlaub.de, alltours, GIATA, or any other travel provider.

The documented source set is TUI Germany, DERTOUR Germany, weg.de, ab-in-den-urlaub.de, and alltours. Upstream endpoints, browser flows, schemas, and commercial terms can change. A successful source can coexist with a failed source in the same run.

## Price and availability limits

- Every price and availability value is a point-in-time website observation.
- A provider can revalidate price, availability, baggage, transfer, taxes, fees, cancellation terms, and room details during checkout.
- Null or `unknown` values must remain unknown. Do not invent missing evidence.
- GIATA-based identity helps normalize hotels, but match quality fields still need to be checked before comparing offers.
- Capacity signals estimate market availability from repeated observations. They do not report hotel occupancy.
- Buy or wait forecasts are informational. They are not price or booking guarantees.
- Repeated polling does not provide continuous real-time coverage.
- No uptime, freshness, accuracy, completeness, or checkout-price SLA is provided by this repository.

## Pricing snapshot

At the audit date, the Store headline started at `$0.70 / 1,000 package offers`. A run could also charge named events for successful source searches and optional comparison, history, airport-matrix, signal, forecast, enrichment, and alert work. The public Example Task selected five sources, so the headline offer price alone was not the complete possible run charge.

Pricing changes over time. Review the Actor's current Pricing tab and set a maximum cost per run before increasing source, result, or airport-matrix limits.

Users are responsible for lawful, proportionate use and compliance with applicable site terms, robots policies, database rights, privacy law, retention rules, and contractual restrictions.
