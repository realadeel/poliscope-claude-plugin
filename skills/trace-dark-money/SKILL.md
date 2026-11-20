---
name: trace-dark-money
description: Trace dark money — documented nonprofit-to-committee flows, 501(c)(4) spending, nonprofit grants and outside spending
argument-hint: <a nonprofit, PAC, candidate, or topic like "gun rights dark money">
---

# Trace Dark Money

Investigate dark money connections for: **$ARGUMENTS**

## Background

"Dark money" is political spending whose original donors aren't disclosed. A typical path:

```
[Donor] --> [501(c)(4) nonprofit] --> [Super PAC] --> [Ads for or against a candidate]
```

The committee reports money from the nonprofit, but the nonprofit's own donors stay hidden. Poliscope shows the documented steps, not the hidden donors.

## Step 1: Entry point

- **A nonprofit:** `search_nonprofits` for its EIN, then `get_dark_money_source` for its documented traces to committees.
- **A committee or super PAC:** `search_dark_money` with its name for traces that end there, and `get_committee` for its receipts and donors.
- **A candidate:** `get_outside_spending` and `list_outside_spending_targets` for independent expenditures for and against them.
- **A topic or overview:** `search_dark_money` with keywords, and `get_dark_money_summary` for totals and the largest sources and destinations.

## Step 2: Map the network

For each nonprofit:
- `get_nonprofit` for its IRS filings, assets, income and officers.
- `get_nonprofit_grants` for the grants it paid, including to other nonprofits.

For each committee:
- `get_committee` for receipts, donors and recipients.
- `get_outside_spending` for its independent expenditures.

## Step 3: Follow grant chains

Some money passes through several nonprofits:

```
[Foundation A] --grant--> [501(c)(4) B] --> [Super PAC C] --> [Candidate]
```

For each grant recipient from `get_nonprofit_grants`, check `get_dark_money_source` with that recipient's EIN.

## Step 4: Other activity

- `get_lobbying_client` shows whether the nonprofit also lobbies.
- `check_relationship` shows documented links between resolved entities.

## Report

### Dark money investigation: [subject]

```
[Nonprofit (EIN)] --$X--> [Committee (FEC ID)] --> [Candidate] (support or oppose)
```

- **Totals traced,** with each trace's method and confidence.
- **Nonprofit details:** income, assets, officers and grants, with filing years.
- **Timing** relative to elections.
- **What can't be seen:** the original donors.

## Evidence rules

- Don't present an inferred trace as a confirmed transfer. Report its method and confidence.
- Officers and grants document roles and payments, not control or intent.
- Cite EINs, FEC committee IDs, entity_ids and amounts from the tools.
