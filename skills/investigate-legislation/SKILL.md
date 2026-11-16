---
name: investigate-legislation
description: Investigate a bill or policy area — sponsors, funding, lobbying, votes, and the interests behind legislation
argument-hint: <bill ID like "HR-118-1234", topic, or policy area>
---

# Investigate Legislation

Research the interests behind: **$ARGUMENTS**

## Step 1: Find the Bill(s)

- **By ID**: `get_bill` with bill_id (format: `TYPE-CONGRESS-NUMBER`, e.g., `HR-118-1234`)
- **By topic**: `search_bills_semantic` for natural-language search (uses embeddings)
- **By keyword**: `list_bills` with search parameter
- Note: bill_id format uses TYPE prefix (HR, S, HJRES, SJRES, HCONRES, SCONRES, HRES, SRES)

## Step 2: Legislative Profile

For each bill:
- `get_bill` — title, summary, status, policy_area, subjects, sponsor
- `get_bill_actions` — full legislative timeline (introduced, committee, floor, signed)
- `get_bill_votes` — roll call votes, party breakdown, margin

## Step 3: Follow the Sponsor's Money

This is the investigative core — who funds the bill's sponsors?

- `get_bill_sponsor_funding` — top contributors to the sponsor's committee
- `get_politician` for the sponsor — full financial profile
- `get_donors_by_employer` — are employees of interested industries donating?
- `check_relationship` between sponsor and major lobbying clients on this topic

For cosponsors: repeat the funding analysis for the top 3-5 cosponsors

## Step 4: Who Lobbied on This?

- `get_bill_lobbying` — entities that specifically lobbied on this bill
- `lobbying_by_topic` — broader lobbying landscape on the policy area
- `list_lobbying_clients` — top spenders on the relevant issue code
- For each top lobbying client: `check_relationship` with sponsor/cosponsors

## Step 5: Outside Spending Connection

- `get_outside_spending` for the sponsor — any independent expenditures?
- `list_outside_spending_targets` — who faced the most outside spending?
- Cross-reference: do outside spenders align with lobbying clients?

## Step 6: Contract Implications

Some bills directly affect government contracting:
- `search_contracts` for companies that lobbied on the bill
- Compare: pre/post-bill contract awards to interested parties

## Report Format

### Legislative Investigation: [Bill Title]

**Bill**: [ID] — [Title] — Status: [current status]
**Sponsor**: [Name] (entity_id) — [Party]-[State]
**Timeline**: [key dates from bill_actions]

**Who wants this bill?**
- Lobbying clients: [list with spend amounts]
- Industry donors to sponsor: [employer-grouped donations]
- Outside spending groups: [if any]

**Who opposes it?**
- Opposing lobbying clients
- Outside spending against sponsor

**Money-vote alignment**:
| Legislator | Vote | Top Industry Donors | Lobbying Contacts |
|-----------|------|--------------------|--------------------|

**Key questions**:
- Did lobbying spending increase before key votes?
- Do the sponsor's top donors benefit from the bill?
- Are there dark money groups involved?

**Citations**: bill_id, entity_ids, vote roll call IDs, dollar amounts with cycles
