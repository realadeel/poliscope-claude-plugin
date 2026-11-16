---
name: research-story
description: Research a news story or political claim using Poliscope data — find evidence, verify claims, add context
argument-hint: <paste a news headline, URL, claim, or story description>
---

# Research Story

Investigate and add data context to: **$ARGUMENTS**

## Step 1: Extract Claims and Entities

Parse the story/claim to identify:
- **Entities**: people, organizations, committees, companies mentioned
- **Claims**: specific assertions that can be verified with financial data
- **Topics**: policy areas, industries, issues involved
- **Time period**: when did this happen?

## Step 2: Resolve All Entities

For every entity mentioned:
- `resolve_entity` to find entity_ids
- Try alternate names if first attempt fails (e.g., "AIPAC" → "American Israel Public Affairs Committee")
- Note: some entities may not be in Poliscope (foreign entities, state-level, private individuals)
- Record which entities resolved and which didn't

## Step 3: Verify Specific Claims

For each verifiable claim, use the appropriate tool:

| Claim type | Tools to verify |
|-----------|----------------|
| "X donated to Y" | `check_relationship`, `get_donor` |
| "X spent $N lobbying" | `get_lobbying_client` |
| "X voted for/against bill" | `get_bill_votes`, `get_legislator_votes` |
| "X traded stock before vote" | `get_trades_by_politician`, `get_bill_votes` |
| "X received contract" | `search_contracts` |
| "Dark money funded X" | `get_dark_money_destination`, `search_dark_money` |

## Step 4: Add Missing Context

What does the story NOT mention that matters?

- `get_bill_sponsor_funding` — who else funds the legislators mentioned?
- `lobbying_by_topic` — who else lobbies on this issue?
- `get_donors_by_employer` — broader employer giving patterns
- `get_outside_spending` — independent expenditure context
- `search_bills_semantic` — related legislation not mentioned

## Step 5: Build the Evidence Package

Categorize evidence:
- **CONFIRMS**: data that supports the story's claims
- **CONTRADICTS**: data that challenges the story's claims
- **ADDS CONTEXT**: data the story missed that changes the picture
- **UNVERIFIABLE**: claims that can't be checked with available data

## Report Format

### Story Research: [Headline/Claim]

**Verdict**: [Confirmed / Partially Confirmed / Unverified / Contradicted]

**Entity Resolution**:
| Name in Story | Poliscope Entity | entity_id | Resolved? |
|--------------|-----------------|-----------|-----------|

**Claim Verification**:
| Claim | Status | Evidence | Source |
|-------|--------|----------|--------|

**Missing Context**:
- [Context point 1 with data]
- [Context point 2 with data]

**Data Limitations**:
- FEC data covers federal only (not state/local)
- Lobbying data from LDA filings (may not capture all activity)
- Dark money traces are incomplete by definition
- Data freshness: most recent cycle available

**Raw Data Links**:
- `https://poliscope.org/politicians/{id}`
- `https://poliscope.org/donors/{id}`
- `https://poliscope.org/committees/{id}`
