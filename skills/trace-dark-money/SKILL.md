---
name: trace-dark-money
description: Trace dark money flows — nonprofit-to-PAC transfers, 501c4 political spending, and undisclosed donor networks
argument-hint: <organization name, nonprofit, PAC, or topic like "gun rights dark money">
---

# Trace Dark Money

Investigate dark money connections for: **$ARGUMENTS**

## Background

"Dark money" = political spending where the original donor is not disclosed. Typical flow:
```
[Wealthy Donor] --> [501(c)(4) Nonprofit] --> [Super PAC] --> [Ads for/against Candidate]
```
The nonprofit doesn't disclose donors. The Super PAC reports receiving from the nonprofit but the ultimate source is hidden.

## Step 1: Entry Point

Determine the investigation direction:
- **Start from a nonprofit**: `resolve_entity` → `get_dark_money_source` (by EIN)
- **Start from a PAC/committee**: `resolve_entity` → `get_dark_money_destination` (by cmte_id)
- **Browse by topic**: `search_dark_money` with keywords
- **System overview**: `get_dark_money_summary` for totals, then `list_dark_money` to browse

## Step 2: Map the Network

For each nonprofit source found:
- `get_nonprofit` + `get_nonprofit_summary` for IRS data (revenue, assets, NTEE code)
- `get_nonprofit_officers` for board/leadership (who controls the money?)
- `get_nonprofit_grants` for outgoing grants (does it fund OTHER nonprofits too?)
- `search_nonprofits` for related organizations (similar names, shared officers)

For each PAC/committee destination:
- `get_committee` for committee details and top contributors
- `get_outside_spending` for independent expenditures (who did they support/oppose?)
- `list_outside_spending_targets` for targeted candidates

## Step 3: Trace Further

- Check if nonprofit officers overlap with lobbyists: `get_lobbying_client`
- Check if the nonprofit is also a lobbying client: `get_lobbying_client`
- Look for corporate connections: `get_company` for parent organizations
- Use `check_relationship` between the nonprofit's officers and politicians

## Step 4: Follow the Grants Chain

Some dark money flows through multiple nonprofits:
```
[Donor] --> [Foundation A] --grant--> [501c4 B] --> [Super PAC C] --> [Candidate]
```
- For each grant recipient in `get_nonprofit_grants`, check if THAT org also appears in `get_dark_money_source`
- Build the full chain

## Report Format

### Dark Money Investigation: [Subject]

**Summary**: Total dark money traced, number of entities involved

**Flow map**:
```
[Nonprofit Name (EIN)] --$X.XM--> [PAC Name (CMTE_ID)]
  Officers: [Name 1], [Name 2]        Spent on: [Candidate] (support/oppose)
  Revenue: $XM | NTEE: [code]
  Also funded by: [Other Nonprofit]
```

**Key actors**: Officers/board members with political connections
**Timing**: When did transfers happen relative to elections?
**Scale**: How does this compare to `get_dark_money_summary` totals?
**Disclosure gaps**: What we can't see (the actual original donors)

**Citations**: Every trace includes EIN, cmte_id, and dollar amounts from the API
