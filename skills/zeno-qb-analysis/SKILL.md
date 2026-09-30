---
name: zeno-qb-analysis
description: Answer financial and operational questions from QuickBooks Desktop through Zeno, choosing QuickBooks reports, the local SQLite mirror, or fixed read tools correctly. Use for statements, balances, aging, profitability, transaction searches, comparisons, rankings, totals, joins, and cross-company questions.
---

# Zeno QuickBooks Analysis

Use the `qb_*` tools from the local Zeno for QuickBooks Desktop MCP server,
and choose one route:

- Use `qb_report` for a statement QuickBooks itself produces: profit and loss,
  balance sheet, trial balance, aging, sales, purchases, or job profitability.
  Do not reconstruct these from transaction lines.
- Use `qb_sync_mirror` then `qb_query` for joins, rankings, custom totals,
  comparisons, and cross-company analysis.
- Use fixed read tools only to resolve names and transaction IDs for posting or
  to answer their narrow listed questions. Do not page through them to build a
  report.

Before relying on a mirror answer, call `qb_mirror_status` and state its
freshness and covered date range. Syncing requires the target company open in
QuickBooks; querying does not. For `allCompanies`, name any registered clients
that were not included because they lack a mirror.

In mirror SQL, aggregate integer `amount_cents` before dividing by 100. Use
`transaction_lines_resolved.effective_account` for account analysis and
exclude display/subtotal lines. Report unresolved account rows, truncation,
inventory-cost limitations, and date-coverage gaps rather than presenting an
incomplete total as final.

State the company, basis, period, mirror freshness, and material exclusions in
the answer. Analysis tools must not write to QuickBooks.
