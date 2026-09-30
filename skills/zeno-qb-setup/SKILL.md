---
name: zeno-qb-setup
description: Set up or diagnose Zeno for QuickBooks Desktop on a Windows workstation, including MCP availability, company discovery and registration, read-only status, and QuickBooks authorization. Use when the user is installing, connecting, adding a client file, or cannot get the first QuickBooks connection to work.
---

# Zeno QuickBooks Setup

Use the `qb_*` tools from the local Zeno for QuickBooks Desktop MCP server.
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

Offer `qb_sync_mirror` followed by a harmless question as the end-to-end test.
Do not post or create anything in QuickBooks during setup.
