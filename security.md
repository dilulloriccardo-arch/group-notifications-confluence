# Security — Group Notifications for Confluence

_Last updated: 2026-09-08_

This page describes the security practices of **Group Notifications for Confluence** ("the app").
The [Privacy Policy](./privacy) is a separate document.

## Architecture
- The app is built on **Atlassian Forge** and is eligible for **Runs on Atlassian**: all code executes
  inside Atlassian's cloud infrastructure. There are **no external servers, no remote endpoints and no
  egress**: the app never makes network calls outside Atlassian.
- No third-party services, SDKs, analytics or advertising libraries are used.
- The app uses only Atlassian product REST APIs (Confluence) through the Forge platform.

## Data handling
- The app reads Confluence group membership and user account IDs only to add/remove page watchers and
  to post @mention comments, and only when an administrator or user explicitly triggers the action.
- Sync rules and an audit log (last 100 actions) are stored in **Forge Storage**, which lives inside
  your Atlassian site's hosting region. This data is deleted when the app is uninstalled.
- The developer has **no access** to any customer site or its data. No customer data ever reaches the
  developer.

## Encryption
- Data in transit between the app and Atlassian APIs travels over TLS within Atlassian's infrastructure.
- Data at rest in Forge Storage is encrypted by Atlassian (see the Forge platform documentation on
  storage). The app stores no secrets, tokens or credentials.

## Permissions (least privilege)
`storage:app`, `read:group:confluence`, `read:user:confluence`, `write:watcher:confluence`,
`write:comment:confluence`. Each scope is justified on the Marketplace Privacy & Security tab. Scheduled
syncs run as the app user and only affect spaces where an administrator has granted the app access.

## Guard rails
- Caps: 250 watchers per manual action, 500 members per rule. Oversized groups are skipped with an
  audit entry, never partially applied.
- Only watchers added by the app are ever removed by the app.
- Every action is written to the audit log visible to site administrators.

## Vulnerability management
- Dependencies are limited to the Forge runtime (Node.js 22) and Forge UI Kit; they are reviewed at
  every release and updated when Atlassian publishes security fixes.
- Every version passes Atlassian's `forge lint` and the Marketplace security review before release.
- **Reporting a vulnerability:** email **security@auftragsregister.ch**. You will receive an
  acknowledgement within **2 business days**. Confirmed issues are fixed and released within
  **30 days** for high severity and **90 days** otherwise; reporters are informed when the fix ships.
- The app is not currently enrolled in the Atlassian Marketplace Bug Bounty Program.

## Incident response
If a security incident affecting customer data were ever identified, affected customers would be
notified through the Marketplace listing and the support address within 72 hours, together with the
impact and the remediation steps.

## Certifications
The app holds no formal security certifications (SOC 2, ISO 27001). It relies on the controls of the
Atlassian Forge platform, which are documented in the Atlassian Trust Center.

## Contact
Riccardo Di Lullo, Zurich, Switzerland — security@auftragsregister.ch (security) ·
dilulloriccardo@gmail.com (general support)
