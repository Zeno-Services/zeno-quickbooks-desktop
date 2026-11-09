---
name: zeno-qb-setup
description: Set up or diagnose Zeno on a Windows workstation, including MCP availability, company discovery and registration, read-only status, and QuickBooks authorization. Use when the user is installing, connecting, adding a client file, or cannot get the first QuickBooks connection to work.
---

# Zeno QuickBooks Setup

Use the `qb_*` tools from Zeno, the local MCP server on Windows.
If they are unavailable, say that the Windows Zeno installer
(zenofirm.com/quickbooks-desktop) must run on the same workstation as
QuickBooks, then the chat client (Claude, the ChatGPT desktop app or Codex)
must be fully quit and reopened. Do not substitute web access or ask the user
to upload a company file.

1. Call `qb_setup` and follow the returned workstation-specific walkthrough.
2. Call `qb_status`. State license and read-only status plainly.
3. Call `qb_discover_companies`. Show candidates, but do not register a guessed
   filename or label until the user confirms it.
4. Register confirmed files with `qb_register_company`. For an exact name and
   path, have the user open the file and use `qb_register_open_company`.
5. Finish with `qb_list_companies` and show what was registered.

QuickBooks permits one open company file at a time. Relay file-switch errors;
do not retry them. First access to each file must be approved in QuickBooks by
the Admin user in single-user mode. If no authorization prompt appears, verify
that condition before troubleshooting anything else. Admin is needed only to
grant the permission: afterwards any user may be signed in, and the login
chosen in the "always allow" dialog is used only when nobody has the file open.

Tell the user about the dialog's personal-data box (Social Security numbers,
card numbers, payroll figures). Zeno uses that data only for QuickBooks' eight
payroll reports, and access to it is a grant a firm should make on purpose:
tick it if they want those reports through Zeno, leave it unticked otherwise.
Everything else works either way, including payroll transactions already in
the books.

If the user picks a dedicated login (a "Zeno" user) for closed-file access,
have them open the file signed in as that user once and set its password
there, then record it. QuickBooks can refuse closed-file connections ("not
protected with a complex password") until that user has set its own password,
even one the Admin chose to meet the rules.

Offer `qb_sync_mirror` followed by a harmless question as the end-to-end test.
Do not post or create anything in QuickBooks during setup.
