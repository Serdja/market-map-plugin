# Market Map connector

Market Map provides read-only market signals derived from configured public Bali Telegram groups about housing, property rentals, transport and local services. These are observed messages in a selected set of chats, not a census of the Bali market or verified transactions. The source groups are selected in the Bali Leads collection configuration. Private messages and closed chats are outside the stated collection scope. Chat names, source-message links and author identifiers are not exposed through the connector. The public response does not provide a per-chat source inventory; coverage can change as configured groups become available or unavailable.

## Connect

Remote HTTP MCP endpoint: `https://tg-leads-landing.vercel.app/mcp`.
No API key or account is required. All five tools are read-only. Set `region` to `bali`, or omit it to use Bali. `phuket` is planned and returns an unavailable status, not Bali data. Every live result includes `region`, `currency`, `status` and `generated_at`.

## Five tools

| Tool | Parameters in addition to optional region | Meaning |
| --- | --- | --- |
| `list_niches_and_areas` | None | Lists public niche IDs, areas currently present in the snapshot, and region statuses. |
| `market_overview` | None | All-time and last-30-day message totals, plus monthly niche series. |
| `niche_demand` | Required `niche` | Niche totals; housing separates seekers, roommates and offers. An unknown niche returns `found: false`. |
| `villa_rent_market` | Optional `area` | 30-day housing demand and offers, plus 90-day seeker budgets and owner offer-price summaries by area. Unknown areas return no data and known areas. |
| `recent_requests` | Optional `niche`, optional `limit` from 1 to 10 | Latest available filtered public request excerpts, up to 10. Empty results mean no matching public excerpt in this snapshot. |

Use the public niche ID (for example `housing` or `bikes`). Legacy IDs ending in `_bali` are also accepted. Area matching accepts names returned by the listing tool and configured Russian/Latin aliases. Niche IDs are not free-text translations.

## 13 niches

| ID | Niche |
| --- | --- |
| `housing` | Housing |
| `bikes` | Motorbike rentals |
| `transfer` | Transfers |
| `beauty` | Beauty services |
| `games` | Games and events |
| `photo` | Photography |
| `auto` | Car rentals |
| `massage` | Massage |
| `visa` | Visa services |
| `handyman` | Handyman services |
| `video` | Videography |
| `wedding` | Weddings |
| `banya` | Bathhouse services |

The public excerpt exporter excludes `games`; that niche may still appear in aggregate counts and in the niche list.

## Areas

Areas are derived from housing geography and budget/price rows, rather than a fixed comprehensive administrative list. The live response checked on 12 October 2026 contained: Berawa (Берава), Bukit (Букит), Kerobokan (Керобокан), Nusa Dua (Нуса Дуа), Pererenan (Переренан), Sanur (Санур), Seminyak (Семиньяк), Seseh (Сесех), Ubud (Убуд), Uluwatu (Улувату), Umalas (Умалас), Ungasan (Унгасан), Canggu (Чангу), and Cemagi (Чемаги). Availability changes with the snapshot. Use the returned spelling; not every Latin alias is configured (for example, use `Унгасан`). Missing area data is not evidence of zero activity.

## Privacy and excerpt filtering

Before public export, detected phone numbers, email addresses, usernames and links are removed, detected author-name tokens are masked, and excerpts with ambiguous names or obfuscated contacts are omitted. This automated filtering is not a guarantee of complete de-identification. Original messages are stored separately by Bali Leads; the connector reads only the filtered public export.

Excerpts are limited to roughly 160 characters at a word boundary. Unsafe or inconclusive excerpts are omitted, so the recent excerpt list is not the full set of messages counted in aggregates. Geography and housing/service requirements can remain in the text; distinctive wording may still be recognizable. Do not use excerpts to identify, contact or profile individuals.

See [the privacy policy](https://tg-leads-landing.vercel.app/privacy) for the separate bot service, original-message storage and deletion requests.

## Refresh and freshness

The exporter defaults to a 60-minute refresh interval, configurable through `PUBLIC_STATS_EVERY_MIN` with a minimum of 15 minutes. It publishes when the process and network are available; this is a schedule, not a freshness guarantee. The MCP server caches a successfully fetched snapshot for up to five minutes. Always inspect `generated_at`; it is the snapshot timestamp, not the time of your tool call. Do not describe an old snapshot as current activity.

Operational observation: when checked on 12 October 2026, the live response reported `generated_at: 2026-10-08T18:14:01.479907+08:00`. The configured hourly schedule was therefore not evidence of an hourly-fresh live snapshot at that check. The cause is not established by this review.

## Budgets versus offer prices

- `demand.budgets_90d` reports what seekers said they were willing to pay. Budgets are not normalized to a common rental period; the API says `not normalized; usually monthly`. Do not label all of them monthly or compare them directly with monthly offers without checking the period.
- `supply.offer_prices_90d` reports extracted owner asking prices normalized to a monthly period; Bali values are IDR, not USD. These are asking prices, not completed rental prices.
- Housing-type totals include seekers and roommates, not offers. A broad area count is not necessarily a count of villa seekers alone.
- Counts represent classified message signals, not verified unique people, signed leases, revenue or willingness to pay for Bali Leads. Respect the sample count attached to summaries; no data is not zero.

Examples: ask for housing demand in Bali, request a rental summary for `canggu`, or fetch three recent `bikes` requests. Describe the snapshot date and keep seeker budgets separate from owner prices.
