---
description: Read live demand for a niche in a region
argument-hint: "[region] [niche]"
---

Read live demand for the requested `region` and `niche` from `$ARGUMENTS`.
Use `bali` as the region only when no region is supplied. Start with
`list_niches_and_areas`; if coverage for the requested region or niche is not
available, explain that and do not infer data.

Call `niche_demand` for the supported niche, then use `recent_requests` only
when examples would materially clarify the result. Report `generated_at` and
describe monetary values honestly: IDR is the currency; a request budget is a
buyer or renter signal, not an offer price; and any offer-price period must be
kept intact.
