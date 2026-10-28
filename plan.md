# PLV-VRS Frontend Implementation Plan

## Product scope

Build a frontend-only React.js web application for PLV-VRS, an AI-assisted campus rule violation reporting and information management system for Pamantasan ng Lungsod ng Valenzuela. The current stage uses mock data and local state only. The frontend uses HTML5, CSS3, TypeScript/TSX as a typed superset of the specified JavaScript/JSX, and Vite on Node.js. The code includes an API service abstraction and typed data contracts so the Laravel 12 JSON REST API and Laravel Sanctum API-token authentication can be connected later without rewriting the interface.

## Design direction options

1. **Academic Civic Console — 0.08 probability:** calm institutional interface with navy, teal, warm paper surfaces, clear status chips, and evidence-oriented cards.
2. **Modern Campus Portal — 0.06 probability:** brighter student-facing interface with larger cards, friendly navigation, and softer blue/green accents.
3. **Compliance Operations Desk — 0.04 probability:** denser administrative workspace with compact tables, stronger dividers, and a more technical monitoring tone.

### Chosen style: Academic Civic Console

- **Design movement:** civic-service editorial UI with restrained institutional polish.
- **Core principles:** trustworthy, calm, legible, privacy-aware, and action-oriented.
- **Color philosophy:** deep navy communicates institutional trust; teal marks safe progress and verified actions; amber marks review or attention; warm off-white surfaces keep the system approachable rather than bureaucratic.
- **Layout paradigm:** a persistent left rail for role-aware navigation, a slim top context bar, and asymmetric content zones that pair a primary work area with a narrow guidance or status rail instead of a generic centered dashboard grid.
- **Signature elements:** small "case signal" eyebrow labels, status chips with explicit meanings, and a consistent evidence/AI provenance treatment that distinguishes original reports from machine suggestions.
- **Interaction philosophy:** every important action explains what will happen next; anonymous-report privacy and due-process reminders appear beside the relevant controls, not hidden in a separate page.
- **Animation:** short, restrained transitions for page changes, drawer opening, status updates, and toast messages; no decorative motion that competes with case information.
- **Typography system:** a highly legible sans-serif UI family with strong numeric readability; hierarchy uses compact uppercase labels, large page titles, and medium-weight body copy. Use a dependable system fallback stack so the project stays self-contained.
- **Brand essence:** a private, accountable reporting channel for a safer PLV campus. Personality: calm, fair, prepared.
- **Brand voice:** direct, respectful, and reassuring. Example microcopy: “Your report is stored securely.” and “AI suggestions require staff confirmation.”
- **Wordmark and logo:** compact PLV-VRS wordmark with a simple shield-and-signal mark built in CSS/SVG so no external asset is required.
- **Signature brand color:** deep PLV navy paired with a distinctive teal verification accent.

## Planned routes and views

- `/` — Sign-in / welcome screen with demo role selector and privacy notice.
- `/student/report` — Student report wizard with identified/anonymous selection, conditional evidence behavior, incident details, and submission confirmation.
- `/student/track` — Tracking page with tracking ID search, status timeline, clarification request form, and privacy explanation.
- `/staff/queue` — OSA/OPD report queue with status filters, search, and priority/review signals.
- `/staff/reports/:id` — Case review workspace with original report, evidence viewer, AI suggestion card, confirm/edit actions, staff notes, and status controls.
- `/committee/cases` — Discipline Committee referred-case view with due-process framing.
- `/admin` — Super Admin overview with user, offense catalog, audit, and identity-access cards.
- `/admin/users` — Role-aware staff account table.
- `/admin/offenses` — Offense catalog table for the 13 minor and 42 major offenses.
- `/admin/audit` — Audit activity table and privileged anonymous-identity access callout.

## Core frontend modules

- `src/app` — route setup, shell, navigation, demo session state, and global styles.
- `src/components/ui` — buttons, inputs, cards, badges, dialogs, tables, timeline, empty states, and toast feedback.
- `src/components/layout` — sidebar, top bar, page header, and responsive navigation.
- `src/features/student` — report wizard, tracking view, evidence rule, and clarification form.
- `src/features/staff` — queue, case review, AI suggestion review, evidence panel, and status controls.
- `src/features/admin` — user management, offense catalog, audit log, and identity-access presentation.
- `src/features/committee` — referred case list and case summary.
- `src/data` — mock users, reports, offenses, audit events, and status histories.
- `src/services` — API client interface with mock adapter now and Laravel adapter boundary later.
- `src/types` — shared report, user, offense, evidence, AI suggestion, status, and audit types.
- `public/manus-routes.json` — route manifest for the managed preview.

## Backend integration boundary

The frontend will not call a database directly. All future data access will go through `src/services/apiClient.ts` and feature-specific service functions. The service boundary exposes the current report methods and reserves `login`, `uploadEvidence`, `listReports`, `getReport`, `reviewAiSuggestion`, `listUsers`, `listOffenses`, and `listAuditEvents` for the Laravel adapter documented in `docs/backend-contract.md`. `VITE_API_BASE_URL` activates the HTTP adapter; an empty value keeps the mock adapter as the default.

The identified/anonymous evidence rule will be enforced in the form state and again at the service boundary: evidence is optional for identified reports and required for anonymous reports. The UI will never expose the Super Admin anonymous-identity view to student, OSA, OPD, or Committee demo roles.

## Implementation and build workflow

1. Create the TODO outcome list from the agreed scope.
2. Build the React/Vite frontend using the agreed HTML5/CSS3 and JavaScript/JSX-compatible stack, with TypeScript/TSX providing typed contracts and self-contained CSS.
3. Implement the route manifest and app shell.
4. Implement mock data and the API service boundary.
5. Implement student reporting and tracking flows.
6. Implement staff, committee, and Super Admin views.
7. Add responsive states and accessible labels/focus behavior.
8. Configure TypeScript diagnostics before the first application-code batch.
9. Run the project on the configured preview port and verify the route manifest.
10. Add the Laravel handoff contract, GitHub Actions CI, and pull-request template.
11. Run typecheck/build checks, inspect the preview, fix confirmed issues, and checkpoint the finished project.

## Out of scope for this stage

- Laravel backend implementation.
- Real authentication, database, file storage, LLM calls, email, or notifications.
- Laravel backend implementation and production deployment.
- Creating or connecting a specific GitHub repository until the team supplies the repository name/account scope or enables the authorized GitHub connector.
