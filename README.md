# Zeno

Bookkeeping in QuickBooks Desktop with a person's review before anything posts.
This plugin teaches Claude, Codex and the ChatGPT desktop app how to work a
QuickBooks Desktop company file through Zeno: set up and register company
files, answer questions from the books, prepare batches of bills, checks,
journal entries, invoices and payments for a person to approve, correct work
that is already posted, and leave a record the next session can pick up.

## What you need

- A Windows PC with QuickBooks Desktop (Pro, Premier, Accountant or
  Enterprise) installed and the company file open.
- Zeno, installed on that same PC from
  [zenofirm.com/quickbooks-desktop](https://zenofirm.com/quickbooks-desktop).
  The installer provides the `qb_*` tools and connects them to Claude, the
  ChatGPT desktop app and Codex. Quit and reopen your chat client after it
  runs.

Without the installed program these skills have no tools to call and will say
so. The company file is read on the workstation and is never uploaded.

## Skills

| Skill | Use it to |
| --- | --- |
| `zeno-qb-setup` | Connect company files, check licence and read-only status, get past the first QuickBooks authorization. |
| `zeno-qb-analysis` | Answer questions: statements from QuickBooks' own reports, anything else from a local SQL copy. |
| `zeno-qb-batch` | Prepare, review, apply and reverse batches. Nothing posts until a person approves. |
| `zeno-qb-corrections` | Fix, void, delete or merge what is already in the books, smallest change first. |
| `zeno-qb-continuity` | Resume pending work, follow playbooks, and record rules, knowledge and the work log. |

Try: "Set up Zeno with my QuickBooks company files", "What did we spend on
fuel last quarter?", or "Show me the batches waiting for review."

## What this plugin runs and sends

This plugin is instructions only. It contains no programs, hooks or MCP server
declarations, runs nothing on install, and sends nothing anywhere.

The tools it describes come from the separately installed Zeno program, which
runs on the workstation and talks to QuickBooks through Intuit's QuickBooks
Desktop SDK. That program keeps its journal and local copy of the books on the
same PC. It makes network calls only for these purposes: one anonymous check
for a newer release at zenofirm.com, and, if the workstation is linked to a
Zeno account for the bank feed add-on, the exchange with api.zenofirm.com that
carries bank transactions to it. The licence check is offline. See the
[privacy policy](https://zenofirm.com/privacy) and
[what it cannot do](https://zenofirm.com/docs/quickbooks-desktop/limits).

## Support

[zenofirm.com/support](https://zenofirm.com/support) or support@zenofirm.com.
Documentation: [zenofirm.com/docs/quickbooks-desktop](https://zenofirm.com/docs/quickbooks-desktop).

This plugin's skill files are MIT licensed (see `LICENSE`). The Zeno for
QuickBooks Desktop program is licensed separately under its end user licence
agreement. QuickBooks is a trademark of Intuit Inc.; Zeno is not affiliated
with or endorsed by Intuit.
