---
name: daily-briefing
description: Generate a political influence briefing — top spenders, active lobbying, recent trades, and dark money activity
argument-hint: [optional: topic focus, cycle, or "latest"]
---

# Daily Briefing

Generate a political influence briefing. Focus: **$ARGUMENTS**

## Data Gathering (run in parallel)

Fetch the following simultaneously:

1. **Campaign Finance**: `list_politicians` (top fundraisers), `list_committees` (top PACs), `list_donors` (top donors)
2. **Lobbying**: `get_lobbying_stats` (totals), `list_lobbying_clients` (top spenders), `list_lobbying_issues` (hot issues)
3. **Dark Money**: `get_dark_money_summary` (totals), `list_dark_money` (recent traces)
4. **Stock Trades**: `list_trades` (recent congressional trades)
5. **Elections**: `get_elections_overview`, `list_election_races` (competitive races)
6. **Outside Spending**: `list_outside_spending_targets` (most targeted candidates)
7. **Legislation**: `list_bills` (recent bills), optionally `search_bills_semantic` for topic focus

If a topic focus was specified, filter/prioritize results related to that topic.

## Report Format

### Political Influence Briefing
*Generated: [date] | Cycle: [current cycle]*

---

**Campaign Finance Snapshot**
- Total raised across top committees: $X
- Top 5 fundraisers with amounts
- Notable donor patterns

**Lobbying Pulse**
- Total lobbying spend: $X (trend: up/down from prior cycle)
- Hottest issue areas by spend
- Top 3 clients and what they're lobbying on

**Dark Money Watch**
- Total dark money traced: $X across N flows
- Largest recent transfers
- Most-funded dark money destinations

**Congressional Trading**
- Recent notable trades
- Any trades in sectors with pending legislation?

**Election Landscape**
- Most competitive races by fundraising differential
- Outside spending hotspots
- Top targeted candidates (support vs oppose)

**Legislation to Watch**
- Bills with most lobbying activity
- Bills with most outside spending connections

---

*All figures sourced from Poliscope API. Entity IDs provided for cross-referencing.*
*Data covers FEC cycles 2000-2026, LDA lobbying, SEC insider transactions, IRS 990 filings.*
