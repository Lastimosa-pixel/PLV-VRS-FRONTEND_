# PLV-VRS Frontend TODO

## Delivered — Frontend foundation and responsive application shell

The React/Vite frontend uses the agreed HTML5, CSS3, JavaScript/JSX-compatible approach, with TypeScript/TSX as a typed superset for maintainable contracts. It provides a professional academic interface with responsive desktop and mobile layouts, role-aware navigation for Student, OSA/OPD Staff, Discipline Committee, and Super Admin demo sessions, and no database, real authentication, LLM, or notification dependency.

## Delivered — Student reporting flow

The Student Portal supports verified-login presentation, Identified or Anonymous report selection, optional evidence for identified reports, required evidence for anonymous reports, incident details, evidence metadata, submission confirmation, and mock tracking-ID generation.

## Delivered — Student tracking and clarification

The tracking page supports tracking-ID lookup, Submitted/Under Review/Under Verification/Resolved status timelines, and clarification submission when a case is Under Verification. Anonymous identity privacy is explained in the student-facing UI.

## Delivered — OSA/OPD case-review workspace

The OSA/OPD queue includes status/date-oriented controls, case review, original report details, evidence panel, AI suggestion with confidence score and summary, Confirm/Edit actions, staff notes, due-process language, and separation of reported allegations from confirmed violations.

## Delivered — Discipline Committee and Super Admin views

The frontend includes a Discipline Committee referred-case view and Super Admin screens for users and roles, the 13 minor and 42 major offense catalog, audit activity, system health, and privileged anonymous-identity access messaging.

## Delivered — Laravel backend handoff

`src/services/apiClient.ts` contains a local mock adapter and a Laravel-ready HTTP adapter with `VITE_API_BASE_URL` configuration, JSON handling, Bearer-token session support, and report tracking, clarification, and status endpoints. `docs/backend-contract.md` defines the planned Sanctum, evidence, anonymity, Gemini, audit, offense-counter, Excel, and DomPDF boundaries.

## Delivered — GitHub-ready setup

The repository includes `.github/workflows/ci.yml` for Node 20/pnpm typecheck and production build validation, a pull-request template, `.env.example` without secrets, and `.gitignore` rules for credentials, dependencies, and build artifacts. A specific GitHub remote still requires the team’s repository name/account scope or authorized connector.

## Delivered — Preview, diagnostics, and delivery readiness

The managed route manifest is available at `public/manus-routes.json`. TypeScript diagnostics are registered, `pnpm typecheck` passes, `pnpm build` passes, and the project is structured for Laravel integration and GitHub collaboration.
