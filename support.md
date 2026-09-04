# Support — Group Notifications for Confluence

- **Email:** dilulloriccardo@gmail.com (response within 2 business days)
- **Issues / feature requests:** open an issue on this repository
- **Documentation:** see the [home page](./) — setup, guard rails, permissions

## Common questions
**A sync rule adds no watchers.** Scheduled syncs run as the app user: grant the app
*space admin* on the target space (Space settings → Permissions → add the app).

**A group is skipped.** Groups above the caps (250 watchers per manual action, 500 members per
rule) are skipped with an audit entry, never partially applied.

**Notifications not received.** Mentions in the footer comment use native Confluence
notifications; check the recipient's notification settings and that they have access to the page.
