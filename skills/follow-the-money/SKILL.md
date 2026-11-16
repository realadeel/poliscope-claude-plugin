---
name: follow-the-money
description: Trace the flow of money between political actors — donations, PAC spending, lobbying, contracts, and dark money
argument-hint: <source and/or destination entity, or a question like "who funds Senator X">
---

# Follow the Money

Trace money flows related to: **$ARGUMENTS**

## Step 1: Identify the Players

- Resolve all entity names with `poliscope:resolve_entity`
- Determine direction: are we tracing money IN (who funds X?) or OUT (where does X spend?)?

## Step 2: Direct Contributions

For money flowing TO a politician/committee:
- `get_politician` or `get_committee` for top contributors
- `list_donors` with entity_id filter for full donor list
- `get_donors_by_employer` to find employer-bundled giving
- `list_employer_totals` for aggregate employer view
- `list_state_totals` + `list_zip_codes` for geographic patterns

For money flowing FROM a donor/company:
- `get_donor` for recipient breakdown
- `search_donors` to find related donors (same employer, coworkers)
- `get_donor_coworkers` for bundling network

## Step 3: Check Direct Relationships

- `check_relationship` between source and destination entities
- This returns: donations (total, count, cycles), lobbying overlap, contract connections

## Step 4: Indirect Money (Dark Money + Outside Spending)

- `search_dark_money` for nonprofit-to-PAC flows
- `get_dark_money_source` (nonprofit EIN) → which PACs received?
- `get_dark_money_destination` (committee ID) → which nonprofits funded it?
- `get_dark_money_summary` for system-wide totals
- `get_outside_spending` for independent expenditures supporting/opposing candidates
- `get_nonprofit_grants` to trace foundation → nonprofit → PAC chains

## Step 5: Spending Side

- `get_spending_summary` for how committees spend money
- `list_spending_vendors` for vendor payments
- `list_spending_trends` for temporal patterns
- `get_spending_vendor` for specific vendor detail

## Step 6: Lobbying as Money

- `get_lobbying_client` to see how much an entity spends on lobbying
- `get_lobbying_firm` to see which firms they hire
- Cross-reference lobbyist clients with campaign contributors

## Report Format

### Money Trail: [Description]

**Flow diagram** (text-based):
```
[Source] --$X,XXX--> [Intermediary] --$X,XXX--> [Destination]
```

**Direct contributions**: amount, count, cycles, top donors/recipients
**Indirect flows**: dark money paths, outside spending, bundling
**Lobbying overlay**: same actors spending on lobbying AND donating?
**Timeline**: when did the money flow? Before/after key votes or contracts?
**Geographic concentration**: where is the money coming from?

**Citations**: every dollar figure must cite the API endpoint + entity_id + cycle
