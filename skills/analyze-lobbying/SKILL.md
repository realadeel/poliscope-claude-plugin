---
name: analyze-lobbying
description: Analyze lobbying activity by topic, client, firm, or legislator — who is lobbying whom on what issues
argument-hint: <topic like "AI regulation", entity name, or question like "who lobbies on defense spending">
---

# Analyze Lobbying

Investigate lobbying related to: **$ARGUMENTS**

## Step 1: Determine Entry Point

**Topic-based** (e.g., "AI regulation", "pharma pricing"):
- `lobbying_by_topic` — maps free-text to LDA issue codes, returns top clients + spend
- `list_lobbying_issues` — browse all issue codes if needed
- `search_bills_semantic` — find related legislation

**Entity-based** (e.g., "Google", "Sen. Warren"):
- `resolve_entity` to get entity_id
- `get_lobbying_client` (if company/org) — who do they hire, how much, what issues?
- `get_lobbying_firm` (if lobbying firm) — who are their clients?
- `get_politician` — check if they receive donations from the same entities

**Bill-based** (e.g., "HR-118-1234"):
- `get_bill` for bill details
- `get_bill_lobbying` — which entities lobbied on this specific bill?

## Step 2: Map the Lobbying Landscape

- `list_lobbying_clients` with issue filter — who are the biggest spenders on this topic?
- `list_lobbying_firms` — which firms dominate this issue area?
- `get_lobbying_stats` — system-wide statistics for context

For each major client found:
- `get_lobbying_client` for their full lobbying profile (spend by year, issues, firms hired)
- `get_company` if they're a public company (revenue context for lobbying spend)

## Step 3: Connect Lobbying to Donations

This is the key investigative step — do lobbying clients also donate to legislators on relevant committees?

- For each major lobbying client:
  - `get_donors_by_employer` — are employees also donating?
  - `check_relationship` between the client and key legislators
  - `get_bill_sponsor_funding` — does the bill's sponsor receive money from lobbying clients?

## Step 4: Identify the Revolving Door

- `get_lobbying_firm` — note lobbyist names
- Cross-reference with `get_legislator` — are former staffers now lobbying?
- Check `get_nonprofit_officers` — do lobbyists sit on nonprofit boards?

## Report Format

### Lobbying Analysis: [Topic/Entity]

**Scale**: $X total lobbying spend, Y registered lobbyists, Z active clients
**Top clients**: ranked by spend with entity_ids
**Top firms**: ranked by revenue on this topic
**Issue codes**: LDA codes matched and their descriptions

**Money-influence nexus**:
| Client | Lobbying Spend | Donations to Relevant Legislators | Bills Lobbied |
|--------|---------------|-----------------------------------|---------------|

**Timeline**: spending trends over cycles (increasing/decreasing?)
**Legislative targets**: which bills attracted the most lobbying?
**Donation overlap**: % of lobbying clients who also donate to relevant committee members

**Citations**: entity_ids, issue codes, bill IDs, cycle ranges
