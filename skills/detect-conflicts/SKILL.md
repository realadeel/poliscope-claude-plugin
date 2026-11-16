---
name: detect-conflicts
description: Detect potential conflicts of interest — stock trades vs committee assignments, donors vs votes, revolving door
argument-hint: <politician name, company, or pattern like "pharma trades">
---

# Detect Conflicts of Interest

Investigate potential conflicts for: **$ARGUMENTS**

## Conflict Pattern 1: Stock Trades vs Committee Jurisdiction

- `resolve_entity` → `get_politician` + `get_legislator` (note committee assignments)
- `get_trades_by_politician` — all stock trades with dates and amounts
- `get_trades_summary` — aggregate trading patterns
- For each traded stock: `get_company` — does this company fall under the politician's committee jurisdiction?
- `get_bill_votes` — did they vote on bills affecting companies they traded?

**Red flags**: trades before committee hearings, trades in regulated industries matching committee assignment, unusual timing around legislative action

## Conflict Pattern 2: Donor-Vote Alignment

- `get_politician` — top donors by industry/employer
- `get_legislator_votes` — voting record
- `get_bill_sponsor_funding` for bills they sponsored
- `get_donors_by_employer` for major employer contributors
- `check_relationship` between top donors and the politician

**Red flags**: consistently voting in favor of top donors' interests, sponsoring bills that benefit major contributors

## Conflict Pattern 3: Lobbying-Legislation Pipeline

- `get_bill_lobbying` — who lobbied on bills the politician sponsored?
- `get_lobbying_client` for those lobbyists — how much did they spend?
- `check_relationship` — do lobbying clients also donate?
- `search_contracts` — did lobbying clients receive contracts?

**Red flags**: sponsor introduces bill → industry lobbies → industry donates → bill passes → industry gets contracts

## Conflict Pattern 4: Revolving Door

- `get_lobbying_firm` — check if former legislators/staffers are registered lobbyists
- `get_nonprofit_officers` — do politicians serve on nonprofit boards after leaving office?
- Cross-reference lobbying firm employees with legislative staff records

## Conflict Pattern 5: Dark Money Influence

- `get_outside_spending` — who spent independently for/against this politician?
- For each outside spender: `get_dark_money_destination` — is it funded by dark money?
- `get_dark_money_source` — trace back to the nonprofit source
- `get_nonprofit_officers` — who controls the dark money nonprofit?

## Report Format

### Conflict of Interest Analysis: [Subject]

**Summary**: X potential conflicts identified, rated by severity

For each conflict:
> **[SEVERITY: HIGH/MEDIUM/LOW]** — [Pattern type]
>
> **What**: [Description of the potential conflict]
> **Evidence**: [Specific data points with amounts and dates]
> **Timeline**: [Sequence of events suggesting conflict]
> **Counterpoint**: [Legitimate explanations, if any]
> **Citations**: [entity_ids, bill_ids, trade dates, dollar amounts]

**Aggregate metrics**:
- % of votes aligned with top donor interests
- Trading volume in committee-jurisdiction stocks
- Lobbying spend from entities that also donate

**Important**: Flag patterns, not guilt. Correlation is not causation. Always note legitimate explanations.
