# Changelog

Public-facing release notes for Aqua Bot. For support or questions, visit our [support server](https://discord.gg/kKaSX5QJwa).

---

## [1.3.13] — 2026-07-16

### Improved
- **Auto backup notifications** — each full backup set now sends only **two** developer/channel embeds: one “Backup Started” with the full task/file inventory in a code block, and one “Backup Completed/Failed” with ZIP sizes, upload success/failure, and retention cleanup. Mid-task upload spam removed.
- **Manual VPS trigger** — create `backups/.run-now` on the server to run a full backup set without disrupting the live bot process

---

## [1.3.12] — 2026-07-16

### Improved
- **`/help`** — simplified to a fast Dyno-style overview embed with link buttons (dashboard, invite, support, vote); removed the command browser dropdown so replies are instant. Full command lists live on the website / dashboard

---

## [1.3.11] — 2026-07-16

### Fixed
- **Timeout hardening pass** — ack watchdog now arms at the start of slash handling (covers slow preflight); `/ping` and other heavy read commands (`/case`, `/rate`, `/setup`, invite-tracker, introduction, modlog, botinfo, warnings/history) always defer before Discord/API work

---

## [1.3.10] — 2026-07-16

### Fixed
- **`/help` timeouts** — command always acknowledges Discord immediately, and help data is built from warm in-memory caches instead of blocking on MongoDB
- **Selective-defer safety** — auto-ack watchdog now defers mid-flight if a command is still working near Discord’s 3-second deadline (fast replies still skip the thinking spinner)

---

## [1.3.9] — 2026-07-16

### Improved
- **Faster simple replies** — configuration and light read commands no longer show a long “thinking…” spinner when they finish quickly; they only defer if work is already close to Discord’s 3-second deadline
- **Moderation feels snappier** — success replies go out right after the action and case are saved; mod-log posts and user DMs continue in the background
- **Ticket close/claim** — interaction acknowledges after the core close/claim work; transcript delivery and claim announcements no longer hold the reply

---

## [1.3.8] — 2026-07-16

### Fixed
- **Global interaction preflight** — command permissions, per-server command rules, ignores, ticket staff, and moderator-role checks now use synchronous snapshots instead of waiting on MongoDB before Discord’s 3-second deadline
- **Remaining command timeouts** — storage-heavy configuration, moderation, ticket, role, tag, and utility commands now defer before slow work while preserving public/private response behavior
- **Autocomplete reliability** — all autocomplete interactions have a guarded 1.5-second deadline; slow data sources safely return no suggestions instead of timing out or double-responding
- **Mongo read resilience** — expired cache entries return immediately and refresh in the background; writes still invalidate and re-read authoritative data
- **Startup safety** — interactions receive an immediate initialization response until all required caches are ready

---

## [1.3.7] — 2026-07-16

### Fixed
- **Application panels** — Apply buttons now open their modal immediately from an in-memory panel cache instead of waiting on MongoDB; eligibility checks run safely after submission
- **Component interactions** — ticket modal buttons, help pagination, ratings, reaction roles, translations, auto-responder menus, and modal submissions now acknowledge before storage or Discord API work
- **Interaction blacklist check** — moved to a periodically refreshed memory cache so a slow database connection cannot consume the 3-second Discord response window
- **Stale components** — unknown/outdated buttons, menus, and forms now receive a clear private error instead of silently timing out

---

## [1.3.6] — 2026-07-15

### Fixed
- **Interaction timeouts** — defer before Discord API / heavy work across moderation, tickets, giveaways, roles, announce, and related slash + button/modal flows so actions no longer finish with “The application did not respond”
- **Reply safety net** — slash commands that forget a final reply now get an error response instead of a silent timeout

---

## [1.3.5] — 2026-07-15

### Improved
- **Stream alerts embeds** — YouTube, Twitch, and Kick footers now show the creator channel name next to the platform (`YouTube • ChannelName • Stream Alerts`); dashboard live preview matches

---

## [1.3.4] — 2026-07-15

### Fixed
- **`/role add` / `/role remove`** — defer the interaction before Discord role API calls so the success reply no longer times out as “The application did not respond”

---

## [1.3.3] — 2026-07-15

### Changed
- **`/slowmode`** — now requires **Administrator** (same as the other admin-only staff commands)

---

## [1.3.2] — 2026-07-15

### Changed
- **Admin-only commands** — `/announce`, `/autoban`, `/autorole`, `/tag`, `/autodelete`, `/poll`, `/lock`, `/unlock`, and `/lockdown` now require **Administrator** (hidden from non-admins; moderator-role bypass cannot unlock them)

### Fixed
- **YouTube stream alerts** — feed titles/dates are parsed per video entry (no more mismatched “old” titles); uploads older than 48h are tracked but never notified; recently seen video IDs are remembered so feed reordering cannot re-alert an older video

---

## [1.3.1] — 2026-07-15

### Fixed
- **Stream & Creator Alerts** — alerts were claimed before Discord send, so failed/silent posts never retried; now roll back and retry until posted
- **Stream & Creator Alerts** — every shard polls its own guilds (no more primary-shard-only skip when sharding grows)
- **YouTube live** — falls back to the public `/live` page when the Data API fails/quota errors
- **Twitch live** — stricter uptime parsing so junk/rate-limit text is not treated as “live”
- **Kick live** — ignores bogus `0001-01-01` start times on offline payloads
- **Dashboard** — requires a notification channel when creators are tracked; clearer setup hints

### Improved
- **Stream alerts** — success/permission-skip logging; already-live creators still alert after being added (video baseline only)

---

## [1.3.0] — 2026-07-14

### Changed
- **Tickets** — removed `/ticket open`; members can only open tickets from a **posted panel** with a configured ticket category
- **Tickets** — close / claim / AFK / rename / move only work inside the matching active ticket channel
- **Dashboard** — ticket panels require a category before save/post; clearer copy that slash open is gone

### Fixed
- **Tickets** — freestyle ticket opens (no panel / no category / channel at guild root) are blocked with clear errors

---

## [1.2.99] — 2026-07-14

### Fixed
- **Supporters Rating** — every vote is stacked into one **final rating** (running average 1.0–5.0⭐ + ratings received); votes are never overwritten; success/leaderboard show this final score clearly

---

## [1.2.98] — 2026-07-14

### Fixed
- **Supporters Rating** — ratings now **stack** into a running average (1.0–5.0⭐) instead of overwriting the previous vote; leaderboard shows star bar + average + “ratings received”; success embeds use the same star visuals

---

## [1.2.97] — 2026-07-14

### Added
- **Supporters Rating** — configurable `/rate` cooldown on the dashboard (seconds / minutes / hours; default still 24 hours)

---

## [1.2.96] — 2026-07-14

### Improved
- **`/rate`** — after picking stars, a **public** channel message announces who rated whom, the star score, and that supporter’s current rank / average / rating count (encourages others to join in)

---

## [1.2.95] — 2026-07-14

### Improved
- **`/rank`** — glossy image rank card (avatar, rank, level, XP bar, total XP, message count) using the same canvas style/colors as level-up cards; falls back to an embed if image generation fails

---

## [1.2.94] — 2026-07-14

### Fixed
- **Stream alerts** — dashboard saves no longer wipe creator live/video tracking IDs (prevents duplicate alerts)
- **Scheduled messages** — locked claim/send counters; dashboard edits cannot clobber `lastSentAt` / `sentCount`
- **Invite tracker / Auto-translate** — settings saves no longer overwrite live stats or tracked messages; untrack + stats reset are explicit actions
- **Automod / Commands / Leveling** — rule Cancel discards; live toggles only write that rule; permissions modal says Close (Save still required); level-up mention edits stay local until Save message
- **Reliability** — moderation case IDs and command defaults use locked updates; module enable checks refresh faster; leave-page warning when settings are dirty

---

## [1.2.93] — 2026-07-14

### Fixed
- **Automod actions** — bot only runs the actions selected for that rule (e.g. Anti-Invite set to Delete message no longer times out users via Anti-Spam lockout or stale punishment lists)
- **Automod rule editor** — **Save rule** persists immediately (the old Done button closed the modal without saving)
- **Automod** — content rules (invite/links/etc.) run before Anti-Spam; dashboard lists live actions on each rule card

---

## [1.2.92] — 2026-07-14

### Fixed
- **Automod** — timeouts/mutes are only claimed after Discord actually applies them (no more “muted” DMs when the member is still chatting); hierarchy + Timeout Members checks; spam soft-lockout keeps deleting/retrying if timeout fails; dashboard timeout duration uses minutes with clearer setup hints

---

## [1.2.91] — 2026-07-13

### Added
- **Supporters Rating** — rate supporters with `/rate` (1–5⭐, 24h cooldown), `/supporter-leaderboard` for staff, configurable reset interval, top-rated role + announce channel, dashboard Reset now
- **Tickets** — multiple panels, each with its own post channel, roles, limits, and appearance (same pattern as application panels)

### Fixed
- **Dashboard errors** — Discord “Missing Access / Missing Permissions / role hierarchy” failures now show plain-language guidance instead of raw API codes
- **Stream & Creator Alerts** — same video/live no longer double-posts (claim-on-write + primary-shard-only polling)

---

## [1.2.90] — 2026-07-13

### Fixed
- **Stream & Creator Alerts** — selecting notification channels immediately marks the form dirty so the Save bar appears (multi-select, no separate Add step)

---

## [1.2.89] — 2026-07-13

### Fixed
- **Stream & Creator Alerts** — notification channels no longer disappear after refresh; bot status updates no longer overwrite channels saved from the dashboard (Mongo cache stale-write race)

---

## [1.2.88] — 2026-07-13

### Added
- **Top.gg voting** — Vote on Top.gg button on `/help`, introduction join messages, and `/botinfo`
- **Website** — “Vote for Aqua” link in the site footer (and homepage product links)
- **Dashboard** — floating “Vote for Aqua” badge (bottom-right, 50% opacity) opens the [Top.gg vote page](https://top.gg/bot/1512880652461150289/vote) in a new tab

---

## [1.2.87] — 2026-07-12

### Improved
- **Logging** — clearer dashboard layout with toggles, per-category enable/disable, and accurate ignore-role filtering copy; moderation logs honor Logging channel mode and event toggle
- **Roles & Joinable ranks** — polished dashboard sections; members use `/joinrank` (admin `/joinablerank` / `/autorole`)
- **Auto Delete** — per-rule enable toggle; dashboard saves no longer wipe pending image-violation timers
- **Slowmode** — full dashboard rule editor: Discord native (0–21600s), shared, and per-user modes, bypass roles, role filters; Discord native applies live on save
- **Image Only** — multi-channel selection, custom warn message with user mention, auto-delete after configurable delay (default 10s), restart-safe pending cleanup
- **Auto Reaction** — multi-channel keyword rules and announcement packs, editable packs, “react to every message” (`matchAll`)
- **Auto Translate** — clearer split between button messages and auto channels; compose flow language picker
- **Scheduled Messages** — clearer status (last/next), ChannelSelect, Start waits one full interval

---

## [1.2.86] — 2026-07-12

### Fixed
- **AFK** — status is now **per-server** (no longer global across all guilds); auto-clear and mention notices run early in message handling so automod/auto-delete/slowmode can no longer skip them

### Improved
- **AFK** — dedicated module with dashboard settings (nickname `[AFK]` prefix, mention cooldown, ignore channels/roles), `/afk status`, relative “away since” timestamps, and migration from legacy global AFK data

---

## [1.2.85] — 2026-07-11

### Fixed
- **Application Panels** — fixed Apply button crash (`Cannot read properties of undefined (reading 'description')`) when a panel had incomplete message settings; review embed defaults are now always filled safely

### Improved
- **Reaction Roles** — dashboard editor rebuilt with the professional full-page editor shell, assignment mode cards, live preview, and clearer panel management

---

## [1.2.84] — 2026-07-10

### Fixed
- **Application Panels** — review embeds now store and show the applicant’s username and display name beside the mention, and post a resolved user mention so reviewers can always identify applicants even after Discord cache refreshes

### Added
- **Reaction Roles** — panel assignment mode: **Toggle** (add/remove) or **One-time claim** (ephemeral error if the member already has the role)

---

## [1.2.83] — 2026-07-10

### Added
- **Tickets** — inside ticket panel embed is customizable from the dashboard panel editor, with live embed preview and static control-button preview
- **Tickets** — ticket control buttons now show emojis and use order: Claim, Re-name, Move, AFK, Close

---

## [1.2.82] — 2026-07-10

### Added
- **Tickets** — server-wide open ticket limit configurable from the dashboard Limits section (0 = unlimited); users see an ephemeral message when the limit is reached

---

## [1.2.81] — 2026-07-09

### Added
- **Leveling** — Maki-style level-up cards with member avatar, accent ring, and generated **level X** image; dashboard toggle between **Level card** and **Custom message**, with card text and color controls

---

## [1.2.80] — 2026-07-09

### Fixed
- **Commands** — full permission metadata audit: hybrid commands (`/ticket`, `/tag`, `/customcommand`) now enforce subcommand permissions centrally; `/moderator` roles grant moderation command access; `/temprole` checks role hierarchy; developer commands hide from non-admins; `/introduction resend` requires Manage Server in the target guild

---

## [1.2.79] — 2026-07-09

### Fixed
- **Giveaways** — fixed a critical bug where large giveaways (e.g. 700+ entries) could send multiple winner announcements with different winners; ending now claims the giveaway atomically before picking winners, and congratulations are announced only once

---

## [1.2.78] — 2026-07-09

### Added
- **Application Panels** — pause or enable each posted panel from its card; the Apply button is disabled/enabled live in Discord without removing the message

---

## [1.2.77] — 2026-07-09

### Fixed
- **Application Panels** — deleting a panel now removes it from the dashboard (legacy `postedPanel` data no longer resurrects deleted panels)
- **Application Panels** — default panel name and placeholders changed from "Content Creator" to **Application Panel**; empty state shows a clear **Create your first panel** button

---

### Fixed
- **Application Panels** — staff review embed editor no longer shows duplicate live previews
- **Application Panels** — if a review message is deleted, stale pending applications are cleared automatically on re-apply; dashboard **Pending** button on each panel lets staff accept, reject, or remove applications

---

### Fixed
- **Application Panels** — new panels ship with default embed title and description; embed builders show placeholders and auto-fill from defaults so saves no longer fail on empty embeds
- **Application Panels** — staff review embed title no longer duplicates "Application" (e.g. "New Content Creator Application" instead of "…Application Application")

---

### Improved
- **Application Panels** — each panel is now fully self-contained with its own approval channel, granted role, reviewer roles, and notification messages (like Auto Responder). Global settings removed; existing configs are migrated automatically.

---

### Improved
- **Application Panels** — applicants who already have the target role see a clear ephemeral message and cannot apply again; missing approval channel or bot permissions return friendly errors instead of crashing; role assignment is validated before accept (Manage Roles + role hierarchy); modal fields can be added or removed per panel (1–5 fields, minimum 1); panel editor label renamed to **Panel Name**

---

### Improved
- **Application Panels** — fixed `{panelName}`, `{user}`, and `{applicationId}` placeholders in staff review embeds; all notification messages now default to embeds; multiple independent panels with per-panel editing; live preview for staff review template

---

## [1.2.71] — 2026-07-09

### Fixed
- **Application Panels** — submitting an application no longer crashes with "Cannot read properties of undefined (reading 'members')"

---

## [1.2.70] — 2026-07-09

### Fixed
- **Application Panels** — dashboard layout no longer overflows the content area; modal submit no longer fails with "client is not defined"

---

## [1.2.69] — 2026-07-09

### Added
- **Application Panels** — post an application embed with an Apply button and customizable modal form; staff review submissions in a dedicated channel with Accept/Reject buttons, role assignment on accept, and configurable private messages (content creator applications and other roles)

---

## [1.2.68] — 2026-07-09

### Improved
- **Admin update broadcast** — faster page load, dedicated progress overlay during sends, and optimized Discord validation

---

## [1.2.67] — 2026-07-09

### Fixed
- **Giveaway participants panel** — faster load and page changes (parallel member lookups, instant defer while fetching names)

---

## [1.2.66] — 2026-07-09

### Fixed
- **Giveaway participants embed** — list is back inside the embed (Giveaway Boat style); each entry shows a mention plus display name/username in parentheses as a fallback when the mention does not resolve

---

## [1.2.65] — 2026-07-09

### Fixed
- **Giveaway participants list** — member names and mentions now display correctly (list moved to message content with resolved usernames; users who left the server show their name instead of a broken ID link)

---

## [1.2.64] — 2026-07-09

### Fixed
- **Level-up announcements** — embed no longer drops when "mention user" is enabled; falls back to the default embed if a custom one fails validation; failures are logged instead of silently ignored

---

## [1.2.63] — 2026-07-07

### Fixed
- **Suggestion reaction emojis** — ✅ and ❌ are always used when fields are empty or unset; custom emojis apply when changed

---

## [1.2.62] — 2026-07-07

### Added
- **Suggestions dashboard** — full embed customization with live preview for posted suggestions and optional private confirmation DMs
- **Multiple suggestion channels** — configure more than one channel from the dashboard or `/suggestion-setup add`
- **Custom reaction emojis** — choose upvote/downvote emojis per server

### Changed
- `/suggestion-setup` now supports `add`, `remove`, and `list` (replacing single `channel` subcommand)

---

## [1.2.61] — 2026-07-06

### Fixed
- **Module & command saves** — batch storage writes for command states and role rules (one request instead of many); command registry preloads when the API starts so the first save is no longer slow
- **Leveling member list** — show display name and username above each user ID again (fetched in parallel for the current page only)

---

## [1.2.60] — 2026-07-06

### Fixed
- **Dashboard saves (logging, modules, commands)** — audit logging no longer blocks API responses (~40 sequential DB writes per logging save caused 30s+ hangs and 500 errors); audit entries are batched and recorded in the background
- **Dashboard load speed** — removed heavy statistics blob from config API; command registry only loads for command/module routes

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
