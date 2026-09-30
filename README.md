# Market Map

Claude Code plugin for reading live, anonymized market signals by region.
**Bali is live; Phuket is planned.** It connects to the public Market Map MCP
endpoint and does not require an API key.

Landing: <https://tg-leads-landing.vercel.app/>

## What it provides

- Demand and supply snapshots by niche and area
- Recent anonymized request signals
- Villa-rental market summaries
- A careful interpretation layer for IDR, periods, budgets, and data freshness

The region is an input to every workflow. If it is omitted, the default is
`bali`; do not silently substitute another region. The connector is designed
to add regions without changing the commands or skill.

## Commands

- `/market-map:market-overview [region]` — a concise regional overview
- `/market-map:niche-demand [region] [niche]` — demand for a niche
- `/market-map:villa-rent-market [region] [area]` — villa-rental signals

Examples:

```text
/market-map:market-overview bali
/market-map:niche-demand bali villa rental
/market-map:villa-rent-market bali canggu
```

## Installation

Install it through your Claude Code plugin workflow, or test a local checkout:

```bash
claude --plugin-dir <plugin-folder>
```

No setup or secret is required: the MCP endpoint is public and read-only.

---

# Market Map — русский

Плагин Claude Code для чтения живых анонимизированных сигналов рынка по
регионам. Сейчас доступны данные по Бали; Пхукет появится позже. Плагин
подключается к публичному MCP Market Map и не требует API-ключа.

Что можно получить: обзор рынка, спрос по нише, недавние обезличенные запросы
и сводку по аренде вилл. Регион передаётся параметром команды; по умолчанию
используется `bali`. Если регион не поддержан, плагин сообщает об этом, а не
подменяет его другим.

Команды и примеры те же, что выше. Для установки секреты и отдельный `SETUP.md`
не нужны: публичный endpoint доступен только на чтение.
