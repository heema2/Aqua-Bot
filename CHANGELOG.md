# Changelog

All notable Aqua Bot updates. Version numbers match production releases.

---

## [1.2.22] — 2026-07-05

### Added
- Immediate server blacklist enforcement when the bot is already in a server (REST + bot queue)
- Dashboard **Sync Required** banner on all guild pages after blacklist removal
- Command sync flag when a server is un-blacklisted while the bot is still present
- Rejoin sync flow when the bot returns to a previously blacklisted server

### Fixed
- Admin panel **Bot not in server** false negative (correct Discord guild API check)
- Blacklist enforcement queue polling interval reduced to 5 seconds as backup

---

## [1.2.21] — 2026-07-05

### Added
- **Logout** button on the Account Blacklisted modal (return to homepage)

---

## [1.2.20] — 2026-07-05

### Changed
- Dev/startup embeds show `username (ID)` for **Added By** on blacklist actions

---

## [1.2.19] — 2026-07-05

### Added
- **Blacklist Users** executive tab — add, edit, remove with pagination (10 per page)
- User blacklist blocks slash commands (ephemeral notice) and dashboard access (modal)
- Duplicate server/user ID rejection on blacklist add
- Paginated **Blacklist Servers** tab (10 per page)

---

## [1.2.18] — 2026-07-05

### Added
- **Blacklist Servers** executive tab — add by server ID + reason, edit, remove
- Bot sends blacklist embed and leaves blacklisted servers on join and startup
- Developer DM + startup channel notifications for blacklist events

---

## [1.2.17] — 2026-07-05

### Added
- Logout confirmation dialog — "Are you sure you want to logout from {user}?"

---

## [1.2.16] — 2026-07-05

### Changed
- Homepage features section shows **9 items** before "Show more" (clean 3×3 grid)

---

## Earlier releases

Prior versions introduced the web dashboard, executive admin panel, stream alerts, auto-translate, server listing, update broadcasts, multi-language dashboard, ticket AFK restore, and the full module suite (moderation, automod, tickets, giveaways, leveling, reaction roles, and more).

See the [live command list](https://www.aqua-bot.xyz/commands) and [website](https://www.aqua-bot.xyz) for current capabilities.
