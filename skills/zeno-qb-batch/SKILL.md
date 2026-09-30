---
name: zeno-qb-batch
description: Prepare, review, apply, or reverse a controlled bookkeeping batch in QuickBooks Desktop through Zeno. Use for bills, checks, journals, card activity, invoices, payments, imports, corrections in volume, pending plans, or any request to post reviewed bookkeeping.
---

# Zeno QuickBooks Batch

Use the `qb_*` tools from the local Zeno for QuickBooks Desktop MCP server.
Treat the review boundary as mandatory.

## Resume Before Creating

Call `qb_list_plans` before preparing overlapping work. Raise reviewed but
unapplied plans first. If resuming a plan, call `qb_review_batch` and show its
current lines and any console exclusions.

## Prepare

1. Resolve uncertain accounts, names, classes, items, invoices, or transaction
   IDs with read tools.
2. Give every entry its real `sourceRef`. Never invent one.
3. Call `qb_plan_batch`. Use `qb_create_names` only after separately showing
   the proposed names and obtaining approval; QuickBooks names cannot be
   deleted afterward.
4. Call `qb_review_batch` as needed and present the complete approval table.
   Do not summarize away blocked, warned, skipped, or already-posted lines.

## Approval Boundary

Stop after showing the plan. Call `qb_apply_batch` with `confirm=true` only
after a human explicitly approves that rendered plan. A clean plan, a host tool
approval dialog, prior model reasoning, or silence is not approval. Do not
combine "plan and post" into one uninterrupted sequence.

Respect reviewer exclusions already recorded in the console. If the plan
changes, show the changed plan and obtain approval again.

## Finish

Report posted, failed, excluded, blocked, and skipped entries separately. Give
the run ID and explain that it is the reversal handle. Record the work and its
source with `qb_log_work`.

Use single-shot write tools only for genuinely one-off corrections. Repeated
single writes bypass batch preflight and automatic idempotency. Transfers are
especially consequential: they have no QuickBooks idempotency key and cannot
be deleted through qbXML.
