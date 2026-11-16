---
name: investigate-entity
description: Build a comprehensive profile of any political entity — politician, donor, company, committee, or nonprofit
argument-hint: <entity name or description>
---

# Investigate Entity

Build a comprehensive profile of **$ARGUMENTS**.

## Step 1: Resolve Identity

- Use `poliscope:resolve_entity` with the name to find entity_id(s)
- If ambiguous, list candidates and pick the best match (or ask)
- Note the `entity_type`: politician, donor, committee, company, nonprofit, lobbying_firm

## Step 2: Core Profile (adapt to entity type)

**Politician**: `get_politician` + `get_legislator` + `get_legislator_votes`
**Donor**: `get_donor` + `get_donor_coworkers` (bundling network)
**Company**: `get_company` + `search_contracts` + `get_lobbying_client`
**Committee**: `get_committee` + `get_spending_summary`
**Nonprofit**: `get_nonprofit` + `get_nonprofit_summary` + `get_nonprofit_grants` + `get_nonprofit_officers`
**Lobbying firm**: `get_lobbying_firm` + `get_lobbying_stats`

## Step 3: Financial Footprint

Run in parallel where possible:
- Campaign contributions: `get_donor` or `get_bill_sponsor_funding`
- Lobbying spend: `get_lobbying_client` or `get_lobbying_stats`
- Federal contracts: `search_contracts` with entity name
- Outside spending: `get_outside_spending`
- Stock trades (politicians): `get_trades_by_politician` + `get_trades_summary`
- Dark money: `get_dark_money_source` or `get_dark_money_destination`
- SEC filings: `search_sec_semantic` for corporate entities

## Step 4: Network Map

- Use `check_relationship` between this entity and any notable connections found
- Use `get_donor_coworkers` for bundling patterns
- Use `get_nonprofit_officers` to find board overlaps
- Use `get_donors_by_employer` for employer-linked giving

## Step 5: Report

Structure the output as:

### [Entity Name] — Profile

**Identity**: type, state, party (if politician), employer (if donor)
**Financial summary**: total raised/spent/donated across all cycles
**Top connections**: ranked by dollar amount with entity_ids
**Notable patterns**: unusual concentrations, timing, or relationships
**Red flags**: conflicts of interest, dark money links, revolving door

**Data citations**: For every claim, include:
- The API endpoint that sourced the data
- Entity IDs for cross-referencing
- Cycle/year ranges covered
- Link format: `https://poliscope.org/politicians/{id}` or `/donors/{id}` etc.
