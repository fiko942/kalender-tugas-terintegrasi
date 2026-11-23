# Initial Application Requirements

## As Is
- The coursework repository at `~/Desktop/Rekayasa Interaksi` contains worksheets and their generation scripts. It has a clean working tree and an existing `origin` remote; it must remain unchanged for this app project.
- No app project exists at `~/Desktop/Kalender Tugas Terintegrasi`.
- The supplied PRD ZIP describes a standalone student task calendar and provides PRD, UX, design, interaction, agent instructions, and 43 acceptance criteria.
- The PRD does not select a framework, hosting provider, authentication vendor, or notification delivery vendor.

## To Be
Create a new standalone, public-GitHub-ready repository rooted at `~/Desktop/Kalender Tugas Terintegrasi`, with a deployable Next.js web application at `apps/web`, a root README containing the PRD, and a root CHANGELOG. The app must support authenticated per-user task CRUD, dashboard, monthly/weekly calendar, task filters and sorting, responsive UX, deadline validation, derived overdue status, and unit/integration coverage. Supabase provides authentication, PostgreSQL persistence, and row-level security. Vercel deployment configuration is included for `apps/web`; production deployment requires user-owned Supabase and Vercel projects/secrets and is not claimed until deployed and verified.

Reminder schedules must be represented and maintained at H-3/H-1 at 09:00 local time, with task changes cancelling/rescheduling pending reminders and duplicate-safe delivery state. This first repository stage will include schema and documented integration boundary; actual outbound delivery requires an explicitly configured provider and deployment secrets. Do not claim reminders are delivered until an end-to-end provider-backed test proves it.

## Requirements
1. The repository is independent from the existing coursework repository and must be suitable for a new public GitHub repository.
2. Root `README.md` must preserve the supplied PRD scope, functional requirements, non-functional requirements, business rules, assumptions, dependencies, out-of-scope items, expected deliverables, and acceptance criteria.
3. Root `CHANGELOG.md` must record this initial stage and clearly identify incomplete external integrations.
4. `apps/web` must be a responsive Next.js App Router application implementing Dashboard, Calendar month/week views, All Tasks filters/sorting, create/edit task, task details, status updates, and confirmed deletion.
5. Task records must be scoped to the authenticated user using Supabase Auth and database row-level security. Secrets must be environment variables and excluded from source control.
6. Task validation must enforce required name/course/deadline, name <=150, course <=100, description <=1000, no past deadlines for new tasks, and default status `Belum Dikerjakan`. Overdue is derived, never persisted as a fourth status.
7. Relevant views must stay consistent after create/update/delete/status change; save failures must preserve entered data and prevent duplicate submits.
8. Calendar must provide month navigation, week view, date selection, today marker, daily task counts, and list all tasks on selected dates.
9. Reminders must have H-3 and H-1 schedule logic at 09:00 in a user-configured IANA timezone, omit past/irrelevant schedules, be cancelled/rescheduled on task changes and completion, and have unique per-task/per-offset identity. Delivery must not be represented as successful absent provider confirmation.
10. Automated tests must cover validation, overdue derivation, filtering/sorting, reminder time calculations and relevant task flows; app must pass lint, tests, and production build.
11. Vercel deployment configuration and setup documentation must target `apps/web`; deployment must be marked pending external account configuration unless actually performed.

## Acceptance Criteria
1. Git status and remotes confirm this app is in a separate repository and the coursework repository remains unchanged.
2. README contains every PRD section and acceptance criterion ID AC-001 through AC-043; CHANGELOG identifies delivered and pending work.
3. `apps/web` renders working dashboard, task list, calendar month/week, and task management views at desktop and mobile widths.
4. Supabase schema enforces authenticated-user task ownership with row-level security policies; unauthenticated requests cannot access another user's task data.
5. Validation, persistence states, empty states, error recovery, delete confirmation, status consistency, overdue derivation, calendar navigation and filtering/sorting work as specified.
6. Reminder schedule calculations generate unique H-3/H-1 at 09:00 local time only when future/relevant; updates/completion/deletion reconcile pending entries. Delivery remains reported as blocked until verified against provider.
7. Unit tests, lint, and production build pass; interactive browser smoke verifies a user flow when browser automation is available.
8. A commit is created in the new repo. A new public GitHub repo receives the commit only after the project has been validated; no changes are pushed to the old repo.

## Testing Plan
- Unit: task validation and overdue derivation; filters/sorting; deadline/timezone reminder calculations; reminder reconciliation invariants.
- Integration: Supabase schema/policies with local or test project when credentials are available; CRUD and save failure duplicate prevention.
- UI/browser: sign in/up, create task, view in dashboard/list/calendar, edit/status update, filtering, delete cancel/confirm, responsive layout, empty/error states.
- Static: lint, type-check, production build.
- Deployment: inspect Vercel configuration and environment-variable documentation; verify live URL only if account configuration is available.

## Implementation Plan
1. Establish isolated app repository and this requirements record; verify the old repository status is unchanged.
2. Add package/configuration and failing domain tests; implement domain validation, filtering, overdue and reminder schedule logic; run tests.
3. Add Supabase schema and RLS tests/documentation; implement typed server/client access and authentication UI; run static checks.
4. Implement responsive app layout and dashboard, task list/detail/form CRUD and confirmations; exercise through browser and tests.
5. Implement month/week calendar, filters/sorts, consistency/error states; test related pages and mobile layout.
6. Add reminder persistence/reconciliation boundary and explicit provider-blocked behavior; test scheduling/cancellation/idempotency.
7. Add root PRD README, changelog, deployment config, and setup instructions; verify full PRD traceability, lint, tests, build, browser flow, then commit and publish to the new public GitHub repo.
