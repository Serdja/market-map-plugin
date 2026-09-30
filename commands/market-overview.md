---
description: Read a live market overview for a region
argument-hint: "[region]"
---

Provide a careful live market overview for the requested `region`. Read the
region from `$ARGUMENTS`; use `bali` only when it is omitted.

First use `list_niches_and_areas` to establish the connector's available
coverage. If the requested region is not available, say so plainly and do not
substitute another one. For an available region, call `market_overview` and
summarize the returned demand, supply, areas, and `generated_at` timestamp.

Follow the Market Map reading rules: state monetary values in IDR, retain the
period attached to an offer price, and never present a request budget as an
offer price.
