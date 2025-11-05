# Repository Guidelines

## Project Structure & Module Organization
Source code lives in `src/`, with feature domains under `src/api/<feature>/{controllers,routes,services,content-types}` (for example `src/api/event/controllers/event.ts`). Shared bootstrap logic sits in `src/index.ts`, while admin tweaks stay in `src/admin`. Runtime configuration is defined in `config/*.ts`, SQLite defaults in `config/database.ts`, database migrations in `database/migrations`, static assets in `public/`, admin builds in `dist/`, and generated types in `types/`.

## Build, Test, and Development Commands
- `npm run develop`: Launch Strapi with auto-reload for local work.
- `npm run start`: Run the compiled app in production mode; use after building.
- `npm run build`: Build the admin panel into `dist/`.
- `npm run console`: Open the Strapi interactive shell for quick data inspection.
- `npm run deploy`: Invoke the Strapi deployment hook.
- `npm run upgrade` / `npm run upgrade:dry`: Apply (or simulate) framework upgrades to the latest Strapi release.

## Coding Style & Naming Conventions
Follow Strapi’s TypeScript presets: two-space indentation, single quotes, and trailing commas where the generator emits them. Keep controllers and services exported as default factories per Strapi conventions. Name content types with lowercase kebab-case folders (`src/api/about`) and PascalCase schemas inside each `schema.json`. Avoid manual edits to files under `dist/` or `types/generated`; regenerate instead.

## Testing Guidelines
No automated suite exists yet. Provide reproducible manual steps and sample requests (for example `curl http://localhost:1337/api/events`). If you introduce Jest or integration tests, store them under `tests/` mirroring the API path (`tests/event/event.test.ts`) and document the new `npm test` command in this guide before merging.

## Commit & Pull Request Guidelines
Commits here favor short imperative subjects (see `git log --oneline`). Group related Strapi file changes in one commit and describe the domain affected (e.g., “Add event ticket URL”). Pull requests should include a concise summary, relevant issue links, environment notes or migration steps, and screenshots of any admin UI changes. Verify builds locally with `npm run build` before requesting review.

## Environment & Configuration
Copy `.env.example` to `.env` and set `DATABASE_CLIENT`, `DATABASE_FILENAME`, and any third-party keys before running the app. SQLite works for local development; switch to Postgres or MySQL by updating `config/database.ts` and providing credentials. Never commit secrets—use environment variables or Strapi Cloud configuration instead.
