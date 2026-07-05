# Changelog

Public-facing release notes for Aqua Bot. For support or questions, visit our [support server](https://discord.gg/kKaSX5QJwa).

---

## [1.2.30] — 2026-07-05

### Added
- **Clone** button on auto responders — duplicate an existing response with all settings; enter a new trigger keyword to save

### Improved
- Auto Responder **create / edit / clone** now opens a dedicated full-page editor (no more editing on top of the list)
- Clearer layout with separate **Trigger**, **Response**, and **Restrictions** sections
- Channel restriction warnings on the editor and response cards

### Fixed
- Could accidentally delete a response while the inline edit form was open

---

## [1.2.29] — 2026-07-05

### Improved
- You can now **rename the trigger keyword** when editing an auto responder (no need to delete and recreate)

---

## [1.2.28] — 2026-07-05

### Fixed
- Auto responders with **allowed channels** set now work reliably when members type in the correct channel
- Auto Responder module state is read correctly after dashboard changes

### Improved
- Dashboard shows which channels an auto responder is limited to
- Warning when **Allowed channels** is set so it is clear the response only works in selected channels

---

## [1.2.27] — 2026-07-05

### Fixed
- Auto responder triggers now match when members type optional symbols before the keyword (e.g. `?web`, `/web`, or `web`)

---

## [1.2.26] — 2026-07-05

### Fixed
- Dashboard **Sync** no longer gets stuck on "Syncing…" when Discord is slow or rate-limited
- Clearer error messages when command sync fails (wait and retry instead of a generic error)

### Improved
- Command sync is faster and more reliable when updating multiple servers

---

## [1.2.25] — 2026-07-05

### Improved
- Bug reports from the dashboard now share the same **1-hour cooldown** as the `/report-bug` slash command

---

## [1.2.24] — 2026-07-05

### Improved
- **Sync Required** badge on the dashboard home page for servers that need a command sync
- Sticky sync banner across all server dashboard pages
- Sync banner restored on the **Commands** page

---

## [1.2.23] — 2026-07-05

### Added
- **Report Bug** — new dashboard page under General to send bug reports to the Aqua Bot team
- **`/report-bug`** slash command — report bugs directly from Discord (title, description, optional command/module)
- Dashboard cooldown indicator so you know when you can submit another report

---

## [1.2.22] — 2026-07-05

### Improved
- Dashboard **Sync Required** banner now appears across all server pages when a command sync is needed
- Better handling when the bot rejoins a server — admins are prompted to sync commands from the dashboard
- General reliability and platform stability improvements

---

## [1.2.21] — 2026-07-05

### Improved
- Dashboard account screens now include a clearer **Logout** option

---

## [1.2.20] — 2026-07-05

### Improved
- Clearer formatting in system status notifications

---

## [1.2.19] — 2026-07-05

### Improved
- Dashboard management pages now use paginated lists for easier browsing
- Improved validation when adding entries to managed lists

---

## [1.2.18] — 2026-07-05

### Improved
- Platform safety and moderation tooling enhancements
- Dashboard management workflow improvements

---

## [1.2.17] — 2026-07-05

### Added
- Logout confirmation — asks you to confirm before signing out of the dashboard

---

## [1.2.16] — 2026-07-05

### Changed
- Homepage features section shows **9 items** before "Show more" for a cleaner layout

---

## Earlier releases

Prior versions introduced the web dashboard, stream alerts, auto-translate, public server listing, multi-language support, ticket improvements, and the full module suite (moderation, automod, tickets, giveaways, leveling, reaction roles, and more).

See the [live command list](https://www.aqua-bot.xyz/commands) and [website](https://www.aqua-bot.xyz) for current capabilities.
