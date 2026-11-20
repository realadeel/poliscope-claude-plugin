---
name: detect-conflicts
description: Check a member of Congress for documented overlaps between stock trades, votes, sponsored bills, donors and lobbying
argument-hint: <member of Congress, company, or pattern like "pharma trades">
---

# Check for Potential Conflicts of Interest

Look for documented overlaps for: **$ARGUMENTS**

This skill finds records that overlap in time or subject. It does not decide whether anything improper happened.

## Step 1: Resolve the member

- `resolve_entity`, then `get_politician` for campaign finance and `get_legislator` for terms, sponsored bills and votes.
- Keep the FEC candidate ID and the Bioguide ID. Trades and votes use the Bioguide ID.

## Step 2: Trades and legislation

- `get_trades_by_politician` for disclosed trades, with dates, owners and amount ranges.
- For each company traded: `get_company` for its lobbying and contracts, and `get_trades_by_ticker` to see other members' trades in the same stock.
- `get_legislator_votes` and `get_bill_votes` show how the member voted on bills that cite or affect that company.
- `get_bill_lobbying` shows whether the company's filings cite those bills.

## Step 3: Donors and votes

- `get_politician` for top contributors and employers.
- `get_donors_by_employer` for giving by employees of companies that lobby on the member's bills.
- `get_bill_sponsor_funding` for each bill the member sponsored.
- `check_relationship` for documented links between a donor and the member.

## Step 4: Outside spending and dark money

- `get_outside_spending` and `list_outside_spending_targets` show independent expenditures for or against the member.
- `search_dark_money` with each spender's name, and `get_dark_money_source` for a nonprofit's EIN, show documented nonprofit-to-committee traces.

## Report

### Potential conflicts: [member]

For each overlap:
- **What overlaps:** for example, a trade in a company whose filings cite a bill the member voted on.
- **Records:** dates, amount ranges, roll calls and filing links.
- **Timing:** the sequence of dates, stated plainly.
- **Other explanations:** for example, a spouse's account, a blind trust, or broad index holdings.

## Evidence rules

- Report overlaps, not guilt. Timing and association don't prove motive or wrongdoing.
- Poliscope doesn't hold committee assignments. Don't assert committee jurisdiction unless a returned record supplies it.
- Trade amounts are reported ranges. Senate disclosures may lag House ones; the tools report freshness.
- Cite entity_ids, Bioguide IDs, roll calls and filing links.
