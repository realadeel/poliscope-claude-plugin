---
name: daily-briefing
description: Generate a political influence briefing — top fundraisers and PACs, outside spending, dark money, lobbying and congressional trades
argument-hint: <optional topic focus, cycle, or "latest">
---

# Political Influence Briefing

Generate a briefing. Focus: **$ARGUMENTS**

## Gather (in parallel where possible)

1. **Scale:** `get_stats` for dataset totals and freshness.
2. **Campaign finance:** `list_politicians` sorted by amount raised for the current cycle, and `list_committees` for the largest PACs.
3. **Outside spending:** `get_outside_spending` for the cycle's totals and top spenders, and `list_outside_spending_targets` for the most targeted candidates.
4. **Dark money:** `get_dark_money_summary` for totals, the largest sources and destinations, and trace methods.
5. **Lobbying:** `lobbying_by_topic` for the focus topic, or for a few current topics if none was given.
6. **Legislation:** `list_bills` sorted by latest action, or `search_bills_semantic` for the focus topic.
7. **Trades:** `get_trades_by_ticker` for tickers tied to the focus, or `get_trades_by_politician` for members in the news.

If a focus was given, keep only results related to it.

## Report

### Political influence briefing
*Generated [date] · Cycle [cycle]*

- **Campaign finance:** top fundraisers and PACs, with amounts and entity_ids.
- **Outside spending:** the cycle total, top spenders, and the most targeted candidates, split into support and oppose.
- **Dark money:** traced totals and the largest documented flows, each with its method and confidence.
- **Lobbying:** the largest clients and issues for the focus.
- **Legislation to watch:** recent bills with their latest action.
- **Congressional trades:** notable disclosed trades, with reported amount ranges.

## Evidence rules

- State each section's cycle or date range and its data freshness. Senate trade disclosures can lag House ones, and the tools say so.
- Trade amounts are reported ranges, not exact values.
- Association isn't evidence of motive or wrongdoing.
- Cite entity_ids and the source links the tools return.
