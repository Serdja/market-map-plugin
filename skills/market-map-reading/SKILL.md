---
name: market-map-reading
description: Read anonymized live market signals from the Market Map MCP carefully. Use for market overviews, niche demand, recent requests, or villa-rental questions by region.
---

# Market Map data reading

Use the public Market Map MCP tools for live, anonymized market signals:

- `list_niches_and_areas` — discover the currently available niche and area
  coverage before making a scoped claim.
- `market_overview` — summarize the market at a high level.
- `niche_demand` — inspect demand for a supported niche.
- `recent_requests` — use recent requests as examples of intent, never as a
  complete market census.
- `villa_rent_market` — inspect villa-rental signals.

## Region handling

Treat `region` as one explicit input to every request. Its default is `bali`.
If a different region is requested, first check live coverage with
`list_niches_and_areas`. If the connector does not return coverage for it, say
that the region has no live data yet; do not replace it with Bali or another
region. This keeps the skill reusable as more regions are added.

## Honest reading rules

- Money is in **IDR** unless the MCP response explicitly states otherwise.
- Preserve an offer-price period exactly: for example, monthly and yearly
  offers are not interchangeable.
- A request's **budget is not an offer price**. Label it as a budget or demand
  signal and do not compare it directly to advertised prices without saying so.
- Include the response's `generated_at` timestamp whenever reporting live
  figures. It tells the reader when the aggregated data was generated, not when
  an individual requester acted.
- Report only fields the tool returned. Say when the sample is limited or a
  niche/area is unavailable; never invent a price, supply count, or trend.

## Response pattern

1. Restate the requested region, niche, and area (when given).
2. Check coverage, then call the narrowest appropriate tool.
3. Present the returned signal with its timestamp and units.
4. Separate demand budgets, offer prices, and descriptive observations.
