---
description: Read villa-rental market signals for a region and area
argument-hint: "[region] [area]"
---

Read villa-rental signals for the requested `region` and optional `area` from
`$ARGUMENTS`. If no region is supplied, use `bali`. Begin with
`list_niches_and_areas`; if that coverage or area is absent, say so rather than
using a nearby area or another region.

Call `villa_rent_market` and, if useful, `recent_requests`. State every money
value in IDR, retain each offer-price period exactly as returned, label request
budgets as budgets rather than prices, and include `generated_at` in the
answer.
