---
name: investigate-legislation
description: Investigate a bill or policy area — sponsors, actions, votes, sponsor funding, lobbying citations and outside spending
argument-hint: <bill ID like "HR-119-1234", a topic, or a policy area>
---

# Investigate Legislation

Research: **$ARGUMENTS**

## Step 1: Find the bills

- **By ID:** `get_bill`. IDs look like `TYPE-CONGRESS-NUMBER`, for example `HR-119-1234`. Types are HR, S, HJRES, SJRES, HCONRES, SCONRES, HRES and SRES.
- **By topic:** `search_bills_semantic` with the user's wording and close synonyms.
- **By keyword, subject or sponsor:** `list_bills`.

## Step 2: Legislative record

For each material bill, `get_bill` gives the title, summary, subjects, sponsor, cosponsors, actions, committees and official text links. `get_bill_votes` gives every roll call with each member's position.

## Step 3: Sponsor funding

- `get_bill_sponsor_funding` for the primary sponsor's campaign-finance context.
- `get_politician` for the sponsor's full profile, and for the main cosponsors.
- `get_donors_by_employer` for giving by employees of organizations that lobbied on the bill.

## Step 4: Lobbying

- `get_bill_lobbying` for filings whose issue text explicitly cites the bill.
- `lobbying_by_topic` for the wider lobbying on the policy area.
- `get_lobbying_client` for the largest clients.

## Step 5: Outside spending and contracts

- `get_outside_spending` and `list_outside_spending_targets` for independent expenditures involving the sponsor and cosponsors.
- `search_contracts` for federal contracts held by organizations that lobbied on the bill.

## Report

### Legislative investigation: [bill title]

- **Bill:** ID, title, status and latest action.
- **Sponsor:** name, party and state, with entity_id.
- **Timeline:** key actions with dates.
- **Votes:** results by chamber and party.
- **Lobbying:** clients whose filings cite the bill, with spending and filing links.
- **Money:** sponsor funding and outside spending, labeled as association only.

## Evidence rules

- A lobbying citation doesn't show support or opposition.
- Contributions don't establish causation or a quid pro quo.
- State the Congresses searched.
- Cite bill IDs, roll calls, entity_ids and filing links.
