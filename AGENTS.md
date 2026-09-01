# AGENTS.md

## Architecture
This is a single-file HTML application (`index.html`). All markup, styles (Tailwind via CDN), and JavaScript logic live in that one file. There is no build step, bundler, or backend — state is persisted client-side via `localStorage` (see keys like `rz_users`, and the `usersDB` in-memory array that mirrors it).

## Key areas in index.html
- Login screen: internal email/password login and optional Google SSO (`handleCredentialResponse`).
- Tabs: Leaderboard, English Hour reporting, Forum, Admin Control Panel (`switchTab`).
- Admin Control Panel → "User & Access Management" modal (`#userManagementModal`): register accounts one at a time (`handleAddUser`), or in bulk via CSV upload (`handleImportUsersCsv` / `parseUsersCsv`). Both paths write into the same `usersDB` array and call `saveUsers()` to persist to `localStorage`.
- Role model: `admin` (full control), `agent` (can submit English Hour reports), `visitor` (read-only). Enforced client-side via `isAdmin`/`isAgent` flags and `applyRole()`.

## Conventions
- No framework/build tooling — keep additions as plain JS/HTML/Tailwind classes inside `index.html`.
- All persistence is `localStorage`; there is no server-side database in this project.
- CSV import is intentionally lenient (skips invalid/duplicate rows rather than failing the whole batch) since this is an internal-use admin tool, not a public-facing form.

## Non-obvious decisions
- CSV parsing is a minimal custom split-on-comma parser (no quoted-comma support beyond simple `"..."` stripping) since the file has no dependency/build system to pull in a CSV library.
- Because everything is client-side, "admin adds users" only means the browser's `localStorage` on the admin's own device gets updated — for durable, multi-device access, this would need to move to real Netlify Identity + Netlify Database.
