# Code review brief

Prepared 2026-10-10 from the workspace attached to this chat.
This describes what is actually in the archive. It is not a legal opinion.

## Bottom line

There is no application in this workspace.

This tree is the stock Grok App Builder starter (package name `app-builder-workspace`).
No pages were written. There is no `src/routes/` directory, so there is no home page,
no API route, no user-authored feature, and nothing a visitor could use.

Nothing here stores or processes a person's data:

- No database has been created for an app. The deploy database flag is off.
- Auth is off. Sign-in is not wired into any page, because there are no pages.
- No `.env` file exists. No user accounts, sessions, uploads, messages, or logs are in this tree.
- No song lyrics, images, or other personal creative files are in this tree.

If the code under review was supposed to be a finished app, it is not in this chat's workspace.
This package cannot stand in for a project from another chat.

## What an analyst will find

| Area | What it is |
|---|---|
| `src/` | Platform helpers only: preview bridge, optional auth, optional database client, optional connector-data client. Not called by any app page. |
| `src/lib/auth/` | Better Auth wiring for "Sign in with Grok". Unused while auth is off. |
| `src/lib/db.ts` | Database client. Unused. No app tables. |
| `src/lib/app-data/` | Helper for reading a viewer's connected services inside a Grok preview. Unused. |
| `migrations/auth/0001_auth.sql` | Stock Better Auth tables (`user`, `session`, `account`, `verification`). Not applied to any app database from this session. |
| `scripts/` | Dev-server, preview, migration, and smoke-test tooling for the builder. |
| `server/middleware/grok-pwa.ts` | Injects the builder's install/branding snippet into HTML. Platform file, not app logic. |
| `public/__grok/` | Default install-page art for the builder. Not app content. |
| `.grok/` | Instructions the builder agent reads while making an app. Not runtime code. |
| `package.json` / `package-lock.json` | Declared dependencies. `node_modules` was not included. |

`.grok/app-env.json` says `"VITE_AUTH_ENABLED": "false"` and `"database": false`.

## Stack (declared, not running as a product)

- Node, Vite 8, React 19, TanStack Start / Router / Query
- Tailwind CSS 4
- Optional, and currently off: Postgres (Neon in production, PGLite locally), Better Auth
- Target host when an app is later published: Vercel

There is no `startup.sh`. That file is only added once an app is actually started.
Nothing was served from this project in this session.

## Deliberate omissions

1. `node_modules/` — third-party packages, reinstallable with `npm ci` from the lockfile. Not original code.
2. One value was removed before packaging: `PREVIEW_CLIENT_SECRET` in `src/lib/auth/preview.ts`.
   It is a platform preview OAuth client secret baked into the starter, not an application secret and not user data.
   The archive has the placeholder `REDACTED_PREVIEW_OAUTH_CLIENT_SECRET` in its place.
   `PREVIEW_CLIENT_ID` remains `grok_preview`. The issuer default in that file is `https://auth.grok.me`.
   No other long-lived credential was found in the source.
3. Empty `screenshots/` was left out. It had no project files.

## What this package is not

- Not evidence of an app's behavior. There is no app behavior.
- Not a copy of any earlier project from another chat.
- Not a dump of environment variables, API keys, session cookies, or a live database.
- The redacted line must not be treated as the original source line.

## How to rebuild the dependencies (if needed)

From the `workspace/` directory, with Node 22: `npm ci`.
That only installs libraries. It does not create an application.
