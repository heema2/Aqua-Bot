# Changelog

Public-facing release notes for Aqua Bot. For support or questions, visit our [support server](https://discord.gg/kKaSX5QJwa).

---

## [1.2.59] — 2026-07-06

### Fixed
- **Dashboard scroll lock** — confirm + success dialogs no longer leave the page unscrollable after leaderboard reset (reference-counted body scroll lock)
- **Leaderboard reset** — faster reset (guild members only); no duplicate success popups; member list reloads only when expanded
- **Dashboard saves** — removed redundant full-guild prefetch on every save; logging config updates tolerate missing log keys; API requests time out with a clear message instead of spinning forever

---

## [1.2.58] — 2026-07-06

### Fixed
- **Leveling reset** — `/reset-leveling` and dashboard reset now correctly await user storage (`listUserIds` was async); reset no longer throws
- **`/backup` commands** — `list`, `stats`, and `config view` defer before slow work; list/autocomplete use local cache first so Discord no longer times out
- **Dashboard performance** — skip heavy guild prefetch on read-only API calls; load config sections in parallel; omit full `statistics.members` from config payload; leveling member panel lazy-loads without per-user Discord API calls
- **Level-up preview** — `{userAvatar}` thumbnail variable resolves in the dashboard preview (no more 404)

### Security
- Re-verified developer-only commands: blocked in `interactionCreate` for slash commands and autocomplete; `/backup` also checks `isDeveloper` at runtime

---

## [1.2.57] — 2026-07-06

### Added
- **`/reset-leveling`** — administrators can wipe all member XP and levels for the server
- **Dashboard leveling control** — paginated member list (10 per page) with editable XP/level, save, and reset leaderboard with confirmation

### Fixed
- **Developer commands** — `developerOnly` and `developersOnly` slash commands now sync only to the support/test guild (`DEV_GUILD_ID`), not every server
- **Booster Thanks embed image** — dashboard and bot now validate Discord-supported image URLs (HTTPS + `.png`/`.jpg`/`.jpeg`/`.gif`/`.webp` or Discord CDN) so test messages show the image correctly
- **Commands page** — shows corrected bot permissions, including per-subcommand bot permissions where applicable (e.g. `/announce`)

---

## [1.2.56] — 2026-07-05

### Fixed
- **Permissions metadata** — `/poll` now declares **Add Reactions** for the bot; `/announce` only requires **Mention Everyone** on the `everyone` and `here` subcommands (not on plain `message` or `role` announcements)

---

## [1.2.55] — 2026-07-05

### Fixed
- **Permissions metadata** — corrected declared bot and command permissions across the codebase so they match what Discord actually requires at runtime
  - `/lock`, `/unlock`, and `/lockdown` now correctly require **Manage Roles** (channel permission overwrites), not Manage Channels
  - `/slowmode` bot checks include Manage Channels (Discord native slowmode) and Manage Messages (shared/user slowmode)
  - `/mute` and `/unmute` bot checks include Manage Roles when using a mute role
  - `/ticket` bot checks include Manage Roles for claim permission updates
  - `/autodelete` user and bot requirements aligned to Manage Messages
- **Invite & website copy** — permission descriptions updated to reflect lock/unlock under Manage Roles

---

## [1.2.54] — 2026-07-05

### Fixed
- **Stream Alerts — Kick** — Kick live detection now uses the official Kick Developer API (`api.kick.com`), which works from VPS hosts where `kick.com/api` was blocked by Cloudflare

### Setup
- Kick alerts require `KICK_CLIENT_ID` and `KICK_CLIENT_SECRET` in the bot `.env` (Kick Developer app — see https://docs.kick.com/)

---

## [1.2.53] — 2026-07-05

### Fixed
- **Giveaways** — fixed active giveaways disappearing and "could not be found" errors caused by stale storage writes wiping giveaway data
- **Invite Tracker** — `{user}`, `{invitername}`, `{totalinvite}`, and other placeholders now resolve correctly in join/leave messages
- **Stream Alerts** — YouTube thumbnail in dashboard preview no longer broken (inline icon)

---

## [1.2.52] — 2026-07-05

### Improved
- **Invite Tracker** — `{totalinvite}` and `{invitername}` variables; default join message shows inviter name and invite count
- **Stream Alerts** — simplified text + role mention editor with live alert preview (no embed builder)
- **Giveaways** — winner count quick-picks (1–10); optional ping winners above congratulations embed on end/reroll

---

## [1.2.51] — 2026-07-05

### Improved
- **Booster Thanks** — live Discord preview beside settings; optional embed image URL and custom embed title
- **Invite Tracker** — customizable join/leave messages (text or embed) with live preview and variables
- **Stream Alerts** — separated notification channels, tracked creators, and per-platform message editors; text or embed prefix with role mentions
- **Giveaways** — prize quick-picks ($10, $50, $100, Premium Package, Battle Pass)

---

## [1.2.50] — 2026-07-05

### Improved
- **Giveaways** dashboard — live Discord preview in the create/edit editor (embed, entry button, requirements)
- **Giveaways** dashboard — main page shows **Start new giveaway** with separate active and ended sections; editor opens in full-page shell

---

## [1.2.49] — 2026-07-05

### Improved
- **Giveaways** dashboard — full-page create/edit editor (same pattern as auto responder and welcome)
- **Giveaways** dashboard — redesigned active giveaway cards with live stats, status badges, and requirement chips

---

## [1.2.48] — 2026-07-05

### Fixed
- **Giveaways** server tag requirement now shows the actual server name and uses “Must use the **ServerName** server tag on your profile.”

---

## [1.2.47] — 2026-07-05

### Fixed
- **Giveaways** dashboard edit no longer resets duration to 1h unless **Edit duration** is checked

### Added
- **Giveaways** — remove ended giveaways from the dashboard list (Discord message unchanged)

---

## [1.2.46] — 2026-07-05

### Added
- **Leveling** — optional “Mention user in channel” on level-up: pings the member with a custom message (e.g. `{user} Congrats!`) above the embed

---

## [1.2.45] — 2026-07-05

### Added
- **Giveaways** — Giveaway Boat–style embeds with prize title, extra entries per role, and requirements block
- **Giveaways** — Required role, blacklist roles, bonus entries per role, and require server tag option
- **Giveaways** — Participants button with paginated ephemeral list in Discord
- **Giveaways** — Weighted entry counts (bonus roles grant extra tickets)
- **Giveaways** — Entry confirmation embed; expired giveaways auto-end on bot restart

### Improved
- **Giveaways** — `/giveaway pause` and `/giveaway resume` now update the Discord message
- **Giveaways** — Dashboard form for all new giveaway options

---

## [1.2.44] — 2026-07-05

### Added
- **Announcements** dashboard paginates sent announcements (10 per page) when the list grows large

---

## [1.2.43] — 2026-07-05

### Added
- **Announcements** dashboard — remove sent announcements from the list without deleting the Discord message

---

## [1.2.42] — 2026-07-05

### Fixed
- **Announcements** dashboard button emojis no longer fail with Discord `Invalid Form Body` — unicode emojis are sent in the correct object format for the REST API

---

## [1.2.41] — 2026-07-05

### Fixed
- **Announcements** dashboard send no longer crashes with `permissions.has is not a function`

---

## [1.2.40] — 2026-07-05

### Fixed
- **Announcements** dashboard send/edit no longer fails with "Failed to read channel permissions (405)" — bot permissions are now computed correctly from channel overwrites and roles

---

## [1.2.39] — 2026-07-05

### Fixed
- **Auto Responder** select menu now works — choosing an option sends the configured bot response ephemerally
- Only the member who triggered the auto responder can use their select menu; others see "You can't use another member's select menu"

### Changed
- Select menu options require a **Bot response** field in the auto responder editor
- **Announcements** dashboard supports buttons only (select menu removed)

---

## [1.2.38] — 2026-07-05

### Added
- **Announcements** dashboard section — send text or embed announcements with buttons, select menus, channel picker, and mention options (@everyone, @here, role, or none)
- Sent announcements appear in history and can be edited while the Discord message still exists
- Permission checks before send (Mention Everyone, Send Messages, Embed Links) with clear dashboard errors

### Fixed
- Welcome module label is now **Welcome** only (no longer combined with Announcements)
- `/announce` command is tied to the new **Announcements** module

---

## [1.2.37] — 2026-07-05

### Added
- **Auto Responder** optional **buttons** and **select menu** on message/embed responses — toggle on in the editor, full validation before save, all fields preserved when re-editing
- **Scheduled Messages** **Start** button on dashboard — new schedules are created stopped; click Start (or `/scheduled-message start`) to activate posting

### Fixed
- Scheduled messages from the dashboard now **save immediately** when added, edited, started, stopped, or deleted — the bot reads them without requiring a separate page save
- Bot scheduled-message processor now checks the **module enabled** state correctly
- `/scheduled-message list` shows all saved schedules including stopped ones

---

## [1.2.36] — 2026-07-05

### Fixed
- **Scheduled Messages** interval field now accepts flexible formats: `30s`, `30 sec`, `10 seconds`, `5 minutes`, `1 hour`, `2 days`, and more
- Repeat count field aligned with interval field (hint moved below input)

### Improved
- Schedule editor shows supported time units, examples, and quick-fill chips for common intervals
- Schedule list displays human-readable intervals (e.g. “every 30 seconds”)

---

## [1.2.35] — 2026-07-05

### Fixed
- **Auto Responder** module toggle no longer flashes disabled on page load
- Auto Responder module enable/disable now requires **Save changes** like every other section page (no instant save on toggle)

---

## [1.2.34] — 2026-07-05

### Fixed
- Level-up message editor now accepts **`{userAvatar}`** in the thumbnail URL field (and shows it in the variables list)

### Improved
- **Module enable/disable toggle** added at the top of every dashboard section page (Logging, Welcome, Auto Responder, Tags, Giveaways, Roles, Reaction Roles, Moderation, and more)
- Consistent **“{Name} Module”** labeling across all section pages
- Amber reminder when a module is **disabled** while editing, plus a notice after saving that settings won't take effect until the module is enabled

---

## [1.2.33] — 2026-07-05

### Improved
- **Leveling**, **Auto Translate**, and **Scheduled Messages** now use the same full-page editor UI as Auto Responder, Welcome, and Tickets
- Level-up message editor opens on its own page with embed colors, links, and images preserved on save
- Auto Translate **send** and **edit tracked message** flows use dedicated editors instead of inline forms
- Scheduled Messages support rich embed editing (colors, images, fields) with full-page create and edit views

### Added
- Scheduled messages can use **text or embed** content from the dashboard (legacy title/description schedules still work)

---

## [1.2.32] — 2026-07-05

### Improved
- **Ticket panel editor** redesigned with the same full-page editor UI as Auto Responder and Welcome
- Panel embed **colors, links, images, author URLs, and fields** are now preserved when you save and re-open the editor
- Wider ticket panel layout for easier editing

---

## [1.2.31] — 2026-07-05

### Added
- **Mention user** option on join welcome embeds — sends `Welcome @user` above the embed so new members get notified
- **Ban announcement** moved to the **Autoban** page — configure ban messages where they belong
- Ban announcements now post automatically when a member is banned

### Improved
- **Welcome & Announcements** redesigned — dedicated editor for join and leave messages (same style as Auto Responder)
- **Autoban** page includes a full ban message editor
- Auto Responder, Welcome, and Autoban editors are **wider** for a better editing experience

### Changed
- Welcome page now only covers **join** and **leave** messages (ban removed from Welcome)

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
