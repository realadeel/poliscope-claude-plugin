---
name: research-story
description: Check a news story or political claim against Poliscope's public records — what the data confirms, contradicts or can't verify
argument-hint: <a headline, claim, or story description>
---

# Research a Story

Check and add context to: **$ARGUMENTS**

## Step 1: Break the claim into parts

List the people and organizations named, each specific claim that public records could test, the topics involved, and the time period.

## Step 2: Resolve every entity

- `resolve_entity` for each name. Try the full name if an abbreviation fails, for example "American Israel Public Affairs Committee" for "AIPAC".
- Record which names resolved and which didn't. State and local actors, foreign entities and private individuals may not be covered.

## Step 3: Test each claim

| Claim | Tools |
|---|---|
| "X donated to Y" | `check_relationship`, `get_donor`, `search_donors` |
| "PAC X gave to candidates" | `analyze_pac_giving` |
| "X spent $N lobbying" | `get_lobbying_client` |
| "X voted for or against a bill" | `get_bill_votes`, `get_legislator_votes` |
| "X traded a stock before a vote" | `get_trades_by_politician`, `get_bill_votes` |
| "X received a federal contract" | `search_contracts`, `get_contract` |
| "Outside groups spent on X" | `get_outside_spending`, `list_outside_spending_targets` |
| "Dark money funded X" | `search_dark_money`, `get_dark_money_source` |

## Step 4: Add missing context

- `get_bill_sponsor_funding` for who funds the legislators involved.
- `lobbying_by_topic` for who else lobbies on the issue.
- `search_bills_semantic` for related legislation.

## Report

### Story check: [headline or claim]

**Result:** confirmed, partly confirmed, contradicted, or can't be verified with these records.

| Claim | Result | Evidence | Source |
|---|---|---|---|

- **Context the story leaves out:** with data and sources.
- **Limits:** for example, federal records only, filings that lag, and dark-money traces that can't show undisclosed donors.

## Evidence rules

- Keep confirmed, contradicted, unsupported and unknown parts separate.
- Records show association, not motive or causation.
- Cite entity_ids and the source links the tools return.
