---
name: follow-the-money
description: Trace the flow of money between political actors — contributions, PAC giving, outside spending, dark money, lobbying and contracts
argument-hint: <source and/or destination, or a question like "who funds Senator X">
---

# Follow the Money

Trace money related to: **$ARGUMENTS**

## Step 1: Identify the players

- `resolve_entity` for each name. Never combine same-named people or organizations without a reviewed identity link.
- Decide the direction: money **into** something (who funds X?) or **out of** it (where does X's money go?).

## Step 2: Direct contributions

**Into a candidate or committee:**
- `get_politician` for a candidate's totals, top contributors and employers, and contribution sizes and geography.
- `get_committee` for a committee's receipts, top donors and recipients.
- `search_donors` for individual contribution records.

**Out of a donor, PAC or company:**
- `get_donor` for an individual donor's recipients by cycle.
- `analyze_pac_giving` for a PAC's complete candidate and party rankings across cycles.
- `get_donors_by_employer` for contributions from a company's employees.

## Step 3: Documented relationships

- `check_relationship` reports documented links between two resolved entities, such as contributions, lobbying and contracts.

## Step 4: Outside spending and dark money

- `get_outside_spending` and `list_outside_spending_targets` cover independent expenditures for and against candidates.
- `search_dark_money` and `get_dark_money_source` show documented traces from nonprofits to political committees.
- `get_nonprofit` and `get_nonprofit_grants` cover a nonprofit's IRS filings and the grants it paid, for chains such as foundation to 501(c)(4) to super PAC.
- `get_dark_money_summary` gives overall totals for context.

## Step 5: Lobbying and contracts

- `get_lobbying_client` for an organization's reported lobbying spending and firms.
- `search_contracts` and `get_company` for federal contracts.

## Report

### Money trail: [description]

```
[Source] --$X--> [Intermediary] --$X--> [Destination]
```

- **Direct contributions:** amounts, counts and cycles, with entity_ids.
- **Indirect flows:** outside spending and dark-money traces, each with its method and confidence.
- **Lobbying and contracts:** the same actors' lobbying spending and federal awards.
- **Timeline:** when the money moved.

## Evidence rules

- Keep candidates, committees, offices and cycles separate. Never move totals between them.
- A dark-money trace documents a recorded path. It can't reveal a nonprofit's undisclosed donors.
- Missing data is unknown, not zero.
- Association isn't evidence of motive, causation or wrongdoing.
- Cite every dollar figure with its entity_id and cycle.
