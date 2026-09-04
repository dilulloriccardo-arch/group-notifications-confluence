# Privacy Policy — Group Notifications for Confluence

_Last updated: 2026-09-04_

**Group Notifications for Confluence** ("the app") is a Forge app that runs entirely on
Atlassian's infrastructure ("Runs on Atlassian"). It has **no external servers, makes no
network calls outside Atlassian, and never sends data to third parties.**

## What the app processes
- Confluence group membership and user account IDs, only to add/remove page watchers and to
  post @mention comments when an admin or user explicitly asks for it.
- Sync rules and an audit log (last 100 actions) that the app itself creates. These are stored
  in Forge Storage **inside your Atlassian site's region**, and are removed when the app is
  uninstalled.

## What the app does NOT do
- No tracking, no analytics, no cookies, no advertising.
- No egress: data never leaves Atlassian cloud.
- No collection of personal data by the developer. The developer has no access to your site's
  data at all.

## Permissions (scopes)
`storage:app`, `read:group:confluence`, `read:user:confluence`, `write:watcher:confluence`,
`write:comment:confluence` — the minimum required for the features above.

## Data retention and deletion
All app data lives in Forge Storage on your site and is deleted on uninstall. You may also
delete individual sync rules and the audit log from the admin page at any time.

## Contact
Riccardo Di Lullo, Zurich, Switzerland — dilulloriccardo@gmail.com
