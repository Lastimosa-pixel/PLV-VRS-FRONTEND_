# PLV-VRS Frontend

A frontend-only React prototype for **PLV-VRS: An AI-Assisted Web-Based Campus Rule Violation Reporting and Information Management System for Pamantasan ng Lungsod ng Valenzuela**.

The interface is designed for the thesis prototype and currently uses mock data. It is structured for a Laravel 12 + MySQL backend and token-based Laravel Sanctum authentication without rewriting the UI.

## Technology stack

| Layer | Technology in this repository | Planned role |
| --- | --- | --- |
| Frontend | React.js, HTML5, CSS3, TypeScript/TSX, Vite on Node.js | Reusable report forms, tracking timeline, staff dashboards, and responsive role-based screens. TypeScript/TSX is a typed superset of the specified JavaScript/JSX and compiles to browser JavaScript through Vite. |
| Backend boundary | Laravel-ready JSON REST adapter | Keeps UI independent from PHP, validation, policies, and persistence. |
| Authentication | Bearer-token session scaffold | Ready for Laravel Sanctum API-token mode. |
| Database | No direct frontend connection | Laravel will own MySQL users, reports, offenses, status histories, confirmed violations, and audit logs. |
| File storage | Multipart endpoint contract | Laravel will keep evidence outside the public web root under randomized names. |
| AI | Structured AI-review endpoint contract | Laravel will call Gemini with only necessary report text and return a staff-reviewable suggestion. |
| Exports | Authorized endpoint contract | Laravel Excel and DomPDF remain backend responsibilities. |

The backend and database are intentionally not included in this frontend repository yet.

## Included views

- Student report flow with Identified and Anonymous modes.
- Conditional evidence rule: evidence is optional for identified reports and required for anonymous reports.
- Tracking ID lookup, status timeline, and clarification submission.
- OSA/OPD review queue and case-review workspace.
- AI suggestion review with confidence score and Confirm/Edit actions.
- Discipline Committee referred-case view.
- Super Admin system overview, user access, offense catalog, and audit activity.
- Protected anonymous-identity and due-process messaging throughout the relevant screens.

## Local development

```bash
pnpm install
pnpm dev
```

The application runs on port `3000` by default. Build and typecheck with:

```bash
pnpm typecheck
pnpm build
```

To activate the Laravel HTTP adapter, copy `.env.example` to `.env` and set:

```env
VITE_API_BASE_URL=http://localhost:8000/api
```

Leave the value empty for mock preview mode.

## Laravel integration

The frontend does not access a database directly. `src/services/apiClient.ts` now contains both a local `mockApi` and a `httpApi` implementation with centralized request handling, Bearer-token support, JSON envelopes, and the report tracking/status/clarification endpoints. The adapter automatically uses `httpApi` when `VITE_API_BASE_URL` is configured.

The complete handoff is documented in [docs/backend-contract.md](docs/backend-contract.md). It covers Sanctum token login, report endpoints, multipart evidence uploads, anonymous identity restrictions, Gemini AI review, offense counters, audit events, and Laravel Excel/DomPDF exports. Laravel must enforce authorization and privacy rules server-side; frontend role navigation is never a security boundary.

## GitHub setup

This repository includes:

- `.github/workflows/ci.yml` for Node 20, pnpm 10.12.4, typecheck, and production build checks.
- `.github/pull_request_template.md` for thesis-team review and backend-contract impact notes.
- `.env.example` without secrets.
- `.gitignore` excluding dependencies, builds, and environment files.

Create a private GitHub repository for the team, then connect and push this project using the team’s authorized GitHub CLI account. Do not commit `.env`, API tokens, Gemini keys, database credentials, or uploaded evidence.

## Project structure

- `src/App.tsx` — role-aware shell and screens.
- `src/styles.css` — academic civic-console visual system.
- `src/types.ts` — shared domain contracts.
- `src/data/mock.ts` — preview users, reports, offenses, and audit data.
- `src/services/apiClient.ts` — mock adapter and Laravel-ready HTTP adapter.
- `docs/backend-contract.md` — frontend/backend endpoint and security handoff.
- `public/manus-routes.json` — managed preview route manifest.
- `plan.md` — implementation and design plan.
- `TODO.md` — delivered outcomes for this frontend stage.

## Prototype note

This stage does not send reports to PLV offices, store files on a server, perform real authentication, call Gemini, or persist data beyond the browser session. Those capabilities belong to the Laravel backend integration.
