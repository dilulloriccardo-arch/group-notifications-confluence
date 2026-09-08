# Group Notifications for Confluence (Forge)

Notify and subscribe **whole Confluence groups** (including IdP-synced ones) — the feature behind
[CONFCLOUD-23015](https://jira.atlassian.com/browse/CONFCLOUD-23015) (802 votes) and
[CONFCLOUD-20118](https://jira.atlassian.com/browse/CONFCLOUD-20118) (519 votes), open since 2010-2011.

## What it does

1. **Notify a group…** (page ⋯ menu → modal): pick a group, then
   - add every member as a **watcher** of the page (native notifications on future edits), and/or
   - post **one** footer comment that @mentions members (immediate native notification; capped at 50 mentions).
2. **Sync rules** (Confluence admin → Group Notifications): keep a group in sync with a page's or space's
   watcher list — joiners start watching, leavers stop. Runs daily (scheduled trigger) or on demand
   ("Run sync now"). Only watchers **added by this app** are ever removed (snapshot diff), so personal
   subscriptions are never touched.
3. **Audit log**: every action recorded (last 100 entries), visible in the admin page.

## Guard rails (enforced server-side, not just in the UI)

- Max 250 watchers per manual action; max 50 mentions per comment; max 500 members per sync rule.
- App/bot accounts are filtered out of member lists.
- Groups over the rule cap are skipped with an audit entry, never partially applied.

## Architecture / platform notes

- **Pure Forge, zero egress** → eligible for the *Runs on Atlassian* badge and the 100% revenue share
  ("fully Forge" incentive). No external services, no LLM API, no containers → platform cost ≈ $0/month.
- UI Kit (`@forge/react`), storage via Forge KVS (`rule:*`, `snap:*`, `audit:log`).
- Scopes: `storage:app`, `read:group:confluence`, `read:user:confluence`, `write:watcher:confluence`,
  `write:comment:confluence`. Nothing else.
- Watching **on behalf of someone else** requires Confluence admin or space admin (REST v1 watch API).
  Manual actions run `asUser` first and fall back to `asApp`; scheduled syncs run `asApp` only, so for
  sync rules the **app user must be granted space admin** on the target space (Space settings →
  Permissions → add the app).

## Things to verify live on the dev site (first deploy checklist)

- [ ] `forge deploy` accepts the manifest (module names checked against docs, but the schema is validated server-side).
- [ ] Storage-format mention markup (`<ac:link><ri:user ri:account-id/>`) triggers mention notifications from a v2 footer comment.
- [ ] `asApp` watcher add succeeds once the app user has space admin; record which permission level is actually required.
- [ ] Group picker returns IdP-synced groups (it should — it lists all site groups).

## Before listing as paid (not needed for the demo)

- Enable licensing in the manifest and check `license.isActive` in resolvers.
- Marketplace Partner account + Partner Verification (**requires a registered business entity** — see `DOMANDA_FORUM.md`).
- Privacy & security tab, EULA (Atlassian template), data-handling statements (this app stores only
  accountIds, group ids/names and audit summaries in Forge storage — no content, no PII beyond accountId).

## Policies
- [Security practices](./security)
- [Privacy Policy](./privacy)
- [Support](./support)
