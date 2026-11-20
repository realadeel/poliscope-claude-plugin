---
name: analyze-lobbying
description: Analyze lobbying activity by topic, client, lobbyist or bill — who lobbies on what, how much they report, and which bills they cite
argument-hint: <topic like "AI regulation", a company or organization, or a bill like "HR-119-1234">
---

# Analyze Lobbying

Investigate lobbying related to: **$ARGUMENTS**

## Step 1: Choose the entry point

**A topic or product** (for example "AI regulation" or "GLP-1 drugs"):
- `lobbying_by_topic` with the user's wording. Keep its match scope: a narrow product query should not grow into a whole LDA issue category.
- `search_bills_semantic` for legislation on the same topic.

**A company or organization:**
- `resolve_entity` for the exact entity.
- `get_lobbying_client` for reported spending by year, issue codes, firms hired, government targets and bills cited in its filings.

**A lobbyist:** `resolve_entity`, then `get_lobbyist`.

**A bill:** `get_bill`, then `get_bill_lobbying` for filings whose issue text explicitly cites it.

## Step 2: Map the landscape

- From the `lobbying_by_topic` results, open the largest clients with `get_lobbying_client`.
- `get_company` adds a company's contracts, SEC filings and political contributions.
- `get_stats` gives overall dataset totals for scale.

## Step 3: Add campaign money

- `get_donors_by_employer` shows contributions from people who list the client as their employer.
- `get_bill_sponsor_funding` shows who funds a cited bill's primary sponsor.
- `check_relationship` reports documented links between a client and a legislator.

## Report

### Lobbying analysis: [topic or entity]

- **Scale:** reported spending, number of filings and clients, and the years covered.
- **Top clients:** ranked by client-reported spending, each with its entity_id.
- **Firms hired:** with registrant-reported income where available.
- **Issues and bills:** LDA issue codes and bills explicitly cited, with filing links.
- **Campaign money:** employee contributions and sponsor funding, labeled as association only.

## Evidence rules

- A filing's amount covers the whole filing. Don't assign all of it to one matched topic.
- A bill citation doesn't show support or opposition.
- Contributions and lobbying document association, not motive or influence.
- Missing amounts are unknown, not $0.
- Cite the LDA filing links and entity_ids the tools return.
