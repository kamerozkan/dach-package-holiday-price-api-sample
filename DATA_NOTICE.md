# Data Notice

## Purpose

This repository is a technical sample for the [DACH Package Holiday Price API Actor](https://apify.com/kamerozkan/dach-package-holiday-price-api). It demonstrates three exact public Example Task inputs, two historical release-QA inputs, privacy-minimized output projections, and machine-readable release evidence.

It is not a booking service, a continuous real-time feed, a complete travel market, or a price guarantee.

## Audit snapshot

The following state was verified through the Apify API and authenticated owner
endpoints on 2026-08-13:

| Item | Verified value |
|---|---|
| Actor | `kamerozkan/dach-package-holiday-price-api` |
| Actor ID | `wgrg8RIdKtTl3x5UT` |
| Public | `true` |
| Latest build at the August 13 audit | `1.0.23`, build ID `cizRcopUm0qBzQUXu`, status `SUCCEEDED` |
| Public Store Example Tasks | 3 |
| Public Example 01 | `XzYQCBdhxElKX9CMM`, `Compare package holidays from Berlin`, slug `compare-package-holidays-from-berlin` |
| Public Example 02 | `1rqXwfhCgJoX6FH19`, `Compare operators for Antalya`, slug `compare-operators-for-antalya` |
| Public Example 03 | `9TDKk28CP93rgNIKu`, `Track Antalya package prices`, slug `track-antalya-package-prices` |
| All-source comparison run | `0q9ttJ7ElPherf6jO`, build `1.0.23`, status `SUCCEEDED` |
| All-source comparison dataset | `oQqXStmQOy6GsawC6`, 3 comparison records from 5 normalized offers |
| All-source comparison platform usage | `$0.003667124558659063` |
| History first run | `X4LBeSIv76YtWKBLA`, 1 new observation, 1 price series, 1 `history-update` event |
| History repeat run | `A5ar96UKEWIwExIZU`, 0 new observations, 0 price series, 0 `history-update` events |
| Historical public task dataset | `ozxjz9utd0IHgwj9l`, 5 records |

Both `latest` and `beta` resolved to build `1.0.23` at verification time. All
five source-health entries in the comparison smoke were healthy and the run
reported no errors. The recovered alltours source reported 300 available
packages and returned one normalized offer. The historical output projections
below remain anchored to their earlier datasets and are not relabeled as output
from the 1.0.23 smokes.

## Input provenance

- [`01_public_berlin_example_input.json`](01_public_berlin_example_input.json) is the exact input exposed by `Compare package holidays from Berlin`.
- [`02_public_compare_operators_antalya_input.json`](02_public_compare_operators_antalya_input.json) is the exact input exposed by `Compare operators for Antalya`.
- [`03_public_track_antalya_prices_input.json`](03_public_track_antalya_prices_input.json) is the exact input exposed by `Track Antalya package prices`.
- [`02_live_offer_qa_input.json`](02_live_offer_qa_input.json) is the exact fixed-date input from a live-source release-QA run completed on 2026-07-26. It remains historical replay material.
- [`03_comparison_forecast_qa_input.json`](03_comparison_forecast_qa_input.json) is the exact fixed-date input from a separate live-source feature-QA run completed on 2026-07-26. It remains historical replay material.

The three public examples use rolling dates. Fixed dates in the historical
replay inputs can expire; replace them with valid absolute dates or rolling
values such as `8 weeks` and `10 weeks` before reuse.

## Release 1.0.23 evidence

[`release_1_0_23_evidence.json`](release_1_0_23_evidence.json) is a
privacy-minimized projection of the verified build, public Examples, comparison
smoke, and history-deduplication smokes. It contains identifiers and aggregate
counts needed to audit these claims, not raw source payloads or credentials.

Run `0q9ttJ7ElPherf6jO` exercised TUI, DERTOUR, weg.de,
ab-in-den-urlaub.de, and alltours with the exact comparison Example input. It
found five offers, wrote three comparison records, reported five healthy
sources, and reported zero errors. This verifies that alltours was producing
normalized output again on build 1.0.23.

Runs `X4LBeSIv76YtWKBLA` and `A5ar96UKEWIwExIZU` reused one isolated history
store with the exact same offer input. The first run inserted one observation,
emitted one price-series row, and charged one `history-update` event. The repeat
run inserted no observation, emitted no duplicate price-series row, and charged
zero `history-update` events. The normal source-search and offer events still
applied to both runs.

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

At the verification date, package-offer pricing was tiered from `$0.70` to
`$1.00` per 1,000 offers by plan. A run could also charge named events for
successful source searches and optional comparison, history, airport-matrix,
signal, forecast, enrichment, and alert work. The five-source comparison Example
therefore costs more than the package-offer headline alone. Its maximum run
charge was set to `$0.10`; the history Example was capped at `$0.02`.

Pricing changes over time. Review the Actor's current Pricing tab and set a maximum cost per run before increasing source, result, or airport-matrix limits.

Users are responsible for lawful, proportionate use and compliance with applicable site terms, robots policies, database rights, privacy law, retention rules, and contractual restrictions.

## Listing update on September 30, 2026

The Store title, description and search metadata were checked against the owned Actor and synchronized with this repository. This documentation update does not alter executable code, input or output schemas, recorded test outputs, artifact hashes, billing or runtime builds. Existing examples retain their original dates and validation limits. A public listing is not evidence of successful output, network acceptance or an achieved search ranking.

## Maintenance evidence on October 4, 2026

[`maintenance-verification-2026-10-04.json`](maintenance-verification-2026-10-04.json) records offline validation of the Actor maintenance across all five providers. Negative/nonfinite required totals and malformed or reversed source calendar dates are rejected. Missing source dates and invalid optional monetary amounts remain null; valid numeric zero is preserved. Calendar-day validation does not validate the complete time/timezone suffix of a timestamp.

The 92 author tests and 17 independent check groups contain synthetic local checks, without new provider calls, source fixtures or customer data in this repository. Separately, public `latest` build `1.0.25` / `9JKFZOpj5ssewuj93` compiled successfully and its server source hashes matched the reviewed package. No new runtime/source run was opened. Neither compilation nor these local tests demonstrates current provider availability, customer output or revenue impact. Pricing, input schema, transport, existing output projections and their historical provenance were not changed by this documentation preparation.

## October 6 billing-description clarification

Only the public billing field description is reconciled with the saved active prices. No prices, validation constraints, defaults or runtime are changed. The check collected no new source data and proves no customer payment or satisfaction. Historical records are preserved.
