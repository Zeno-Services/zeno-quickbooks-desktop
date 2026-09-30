---
name: zeno-qb-corrections
description: Fix, void, delete, or merge what is already in QuickBooks Desktop through Zeno, and update cleared status. Use when a posted transaction is wrong, a duplicate name needs merging or removing, a record needs a field changed, or the user asks to undo, remove, or correct existing bookkeeping.
---

# Zeno QuickBooks Corrections

Use the `qb_*` tools from the local Zeno for QuickBooks Desktop MCP server.
This is the riskiest surface in the product: everything here changes or
removes work that already exists, some of it with no way back. Slower is
correct.

## Choose the Smallest Verb

In order of preference:

1. **Modify** (`qb_modify_transaction`, `qb_modify_customer`, and the other
   `qb_modify_*` tools) — changes fields in place and journals what was
   replaced, so the old figures remain recoverable by reading.
2. **Void** (`qb_void_transaction`) — zeros the amounts but keeps the numbered
   record in the register and the audit trail. Prefer it over delete for
   anything that was real and is now wrong.
3. **Delete** (`qb_delete_transaction`) — removes the record entirely, with no
   undo. Use only for something that should never have existed, and say so
   before asking approval. Transfers cannot be deleted or voided through
   qbXML at all; time entries and mileage can only be deleted, never voided.
4. **Reverse a run** (`qb_reverse_run`) — the right verb when the mistake is a
   whole batch this product posted. It undoes in the only order QuickBooks
   accepts and picks void or delete per kind itself.

If a correction arrives in volume — twenty wrong dates, a month recoded — use
`qb_plan_batch` and the review boundary instead of twenty single calls.

## Preview, Then Confirm

`qb_modify_transaction` with `confirm=false`, `qb_merge_duplicates` with
`confirm=false`, and `qb_delete_list_entry` with `confirm=false` change
nothing and return exactly what would happen. Always show that preview.
`confirm=true` means a person read it and said yes — never that the preview
looked clean. Do not fetch a preview and confirm in one uninterrupted
sequence.

Never carry an EditSequence across turns. The modify tools read the current
one in the session they write from; a sequence fetched earlier is stale by
design, and 3200 is the refusal that says so.

## Names and Lists

- **Merge** (`qb_merge_duplicates`) is the one operation with no undo of any
  kind — say so, suggest a backup first, and get the direction right:
  `mergeFrom` disappears. Requires single-user mode; refused while an
  accountant's copy exists. Afterwards run `qb_sync_mirror` with
  `rebuild=true` — a merge rewrites history without marking it modified.
- **Delete a list record** (`qb_delete_list_entry`) only works on records with
  no history; QuickBooks refuses the rest with 3160. That makes it right for
  the typo vendor created yesterday and wrong for anything used — merge or
  deactivate those (the `qb_modify_*` tools set inactive).

## Read the Refusal Before Retrying

- **Retry after re-reading:** 3200 (record changed under you — run the
  preview again and show it again).
- **Fix and retry:** 3120/3130/3140 (a name did not resolve — use the read
  tools), 3150 (a required field).
- **Stop and tell the user, do not retry:** 3161/3171 (closing date — the
  Admin holds that password), 3175/3176 (someone has it open in the
  QuickBooks window), 3162 (single-user mode needed), 3260-series
  (permissions), and any repeated failure that mentions a modal dialog —
  that needs a human at the QuickBooks machine.

`qb_doctor` reports the file's user mode and any accountant's copy before
anyone is mid-task; run it when corrections keep being refused.

## Finish

Report exactly what changed, quoting TxnIDs and the run journal's ids. A
void or delete of a posted transaction, and every merge, deserves a
`qb_log_work` entry carrying the reason — the journal keeps what happened,
and nothing but the work log keeps why.
