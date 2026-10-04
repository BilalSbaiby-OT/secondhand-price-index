# Resale IQ Secondhand Price Index

A monthly, open dataset of **median asking prices** and **observed departures** for tracked fashion brands and categories on Vinted in France, Germany, Spain, Italy and Portugal. Published by [Resale IQ](https://resaleiq.dev/data/secondhand-price-index).

Aggregates only. No listing-level data, no model-level verdicts, no code.

## Cite as

> Resale IQ Secondhand Price Index, October 2026, resaleiq.dev/data/secondhand-price-index

Licence: [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). Reuse freely with attribution to "Resale IQ".

## Files

- `data/secondhand-price-index-YYYY-MM.csv`: one edition (data month YYYY-MM, published the month after).
- `data/secondhand-price-index-latest.csv`: copy of the newest edition.
- `CHANGELOG.md`: what changed per edition.

## Columns

| column | meaning |
|---|---|
| `month` | data month (YYYY-MM) |
| `level` | `market_total`, `brand_market`, `category_market`, `brand_all` or `category_all` |
| `market` | `fr`, `de`, `es`, `it`, `pt` or `all` |
| `brand`, `category` | blank when not applicable to the level |
| `departures_n` | observed departures in the cell (the sample size) |
| `median_asking_eur`, `p25_asking_eur`, `p75_asking_eur` | median and middle-half range of asking prices in euro |
| `departure_share_pct` | cell departures ÷ all departures in the same market (or all markets) |
| `demand_index` | cell departures ÷ the top cell of the same table and market × 100 |
| `mom_median_pct`, `mom_demand_index_pts` | month-over-month change; empty until a prior full month exists |

## Definitions

- **Observed departure**: a listing our crawler saw on a Vinted shelf and later saw leave it. Not a confirmed sale: it can also be a delisting, an offline sale or a relist. We never see the price a buyer paid.
- **Asking price**: the price on the listing the last time we saw it, converted to euro. What the seller asked, not what anyone paid.
- **Demand index**: ranks cells inside our sample. It is not a market share.
- **Minimum sample**: a cell is published only with at least 30 observed departures. Smaller cells are omitted, not estimated.

## Method

The crawler re-reads public Vinted shelves about every 30 minutes and records which listings disappear. Per edition we keep departures of tracked brands, drop deleted listings, the catch-all category and departures whose brand does not match the shelf that ended them, and count an item once per market. Full method: https://resaleiq.dev/methodology

## Limits

Only tracked brands and categories. Observed departures are a lower bound. Tracking began on 30 August 2026, so September 2026 is the baseline edition without month-over-month change.
