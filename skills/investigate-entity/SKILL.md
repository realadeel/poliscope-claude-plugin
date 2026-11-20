---
name: investigate-entity
description: Build a source-backed profile of a politician, donor, company, committee, lobbyist or nonprofit
argument-hint: <entity name or description>
---

# Investigate an Entity

Build a profile of **$ARGUMENTS**.

## Step 1: Resolve the identity

- `resolve_entity` with the name. If several candidates match, list them and ask which one is meant, or choose by exact identifiers such as state, EIN or FEC ID.
- Separate same-named entities stay separate.

## Step 2: Core profile, by type

- **Politician:** `get_politician` for campaign finance, then `get_legislator` and `get_legislator_votes` for congressional activity.
- **Donor:** `get_donor` for recipients by cycle.
- **Company:** `get_company` for lobbying, contracts, contributions and SEC records. Add `get_lobbying_client`, `search_contracts` and `get_sec_company` for detail.
- **Committee or PAC:** `get_committee`, plus `analyze_pac_giving` for its giving across cycles.
- **Lobbyist:** `get_lobbyist`.
- **Nonprofit:** `search_nonprofits` for the EIN, then `get_nonprofit` for filings and officers, and `get_nonprofit_grants`.

## Step 3: Financial footprint

Where it applies:
- Campaign giving or receipts: `get_donor`, `get_politician` or `get_committee`.
- Employee giving: `get_donors_by_employer`.
- Lobbying: `get_lobbying_client`.
- Federal contracts: `search_contracts`, then `get_contract` for detail.
- Outside spending: `get_outside_spending`.
- Dark money: `search_dark_money` and `get_dark_money_source`.
- Congressional trades: `get_trades_by_politician` for members, or `get_trades_by_ticker` for a company's stock.
- SEC filings: `search_sec_semantic` and `get_sec_company`.

## Step 4: Connections

- `check_relationship` between this entity and each notable connection found.

## Report

### [Entity name]

- **Identity:** type, state, party for politicians, and exact identifiers.
- **Financial summary:** totals by cycle or year, each with its coverage.
- **Top connections:** ranked by amount, with entity_ids.
- **Notable patterns:** concentrations and timing, stated as documented facts.

## Evidence rules

- Report only what the returned records show. Don't add background such as headquarters or committee assignments unless a record supplies it.
- Association isn't evidence of motive or wrongdoing.
- Link pages as `https://www.poliscope.org/politicians/{id}`, `/donors/{id}` and `/committees/{id}`, using the IDs the tools return.
