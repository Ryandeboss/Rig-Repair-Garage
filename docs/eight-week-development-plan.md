# My Rig Eight Week Development Plan

Rig Repair Connect | Apex Summit LLC | Prepared October 27 2026

Ryan and Ibrahim will build My Rig as an isolated Garage module in one GitHub repository. This plan defines what to build, who owns it, what proves it works, and when each milestone is reviewed. The eight-week outcome is a working development Garage with persistent truck and maintenance data, not a production launch of every future RRC service.

### Proposed dates and capacity

Kickoff is Monday November 2 2026. Week 8 ends Sunday December 27, with final acceptance on Wednesday December 23. Dates and assignments are proposed until Ryan and Ibrahim confirm availability at kickoff. All deadlines are 6 PM America Chicago time.

Budget 14 hours per person in each normal week and 8 hours in each holiday week. Feature estimates total 129 hours: Ryan 62 and Ibrahim 67. Reserve 28 more team hours for planning/review and about 43 hours for integration, learning and unexpected fixes. These are planning estimates, not a guarantee of delivery.

### What is included

Truck list and dashboard; add/edit truck; dated mileage/engine-hour readings; component details; multi-item service records and corrections; custom maintenance plans; status/sorting; attributed demo recommendations; mobile layouts; a separate development login/database/API; CI, previews and a repeatable acceptance flow.

### Later backlog

Paid expert reviews and assignment; real Rig Health Report authoring; asynchronous paid questions; live calling; Stripe/Twilio integration; subscriptions/fleets; real OEM schedule ingestion; predictive maintenance; parts/affiliate commerce; receipt/photo uploads; reminder delivery; and integration into the production RRC marketplace.

Truck imagery uses bundled assets in this plan. “Reminders” means on-screen upcoming maintenance only; no email/SMS scheduling is promised. A sample report is optional and read-only.

### Where the work lives

Repository: https://github.com/Ryandeboss/Rig-Repair-Garage. The current repo contains the README only. This schedule refines the earlier conceptual milestones into eight weekly gates. No application or hosting configuration is created by this planning document.

## Schedule and ownership

Feature deadlines below mean ready for review, with tests and a PR. The milestone gate is the acceptance deadline after review, fixes and a deployed demonstration. Each feature card later in the plan has its own earlier PR deadline.

| Week | Dates 2026 | Milestone | Gate |
| --- | --- | --- | --- |
| 1 | Nov 2 to Nov 8 | Foundation and shared contracts | Nov 06 |
| 2 | Nov 9 to Nov 15 | Truck management and mileage | Nov 13 |
| 3 | Nov 16 to Nov 22 | Maintenance records and history | Nov 20 |
| 4 | Nov 23 to Nov 29 | Maintenance timing and attention sorting | Nov 25 |
| 5 | Nov 30 to Dec 6 | Isolated backend and persistent truck data | Dec 04 |
| 6 | Dec 7 to Dec 13 | Persistent maintenance and complete user flow | Dec 11 |
| 7 | Dec 14 to Dec 20 | Recommendations and release hardening | Dec 18 |
| 8 | Dec 21 to Dec 27 | Acceptance fixes and handoff | Dec 23 |

### Ryan owns

Product scope, shared data and API contracts, status rules, backend, database/auth and access controls, CI/CD settings, staging resources, migrations and final acceptance. Ryan reviews and merges Ibrahim PRs. He creates PRs for his own work too; Ibrahim checks the user-facing behavior and asks questions.

### Ibrahim owns

Dashboard and truck/component cards, forms, history/detail screens, recommendation presentation, API-adapter UI integration, mobile/accessibility checks and the browser acceptance suite. He owns tests and bug fixes for these features, not just their first implementation.

### Shared decisions

Agree on types, expected behavior and mock examples before splitting work. Do not independently rename shared fields or update shared dependencies. Use one active feature per person; split a task if it grows beyond a few focused sessions.

### Dependency rule

A UI task can start against its agreed mock contract while an upstream implementation is in progress. It cannot be accepted until the declared dependencies pass. If a gate fails, hold dependent integration and replan; unrelated UI work may continue.

## Feature assignment index

All dates are 2026. PR due means ready for review by 6 PM America Chicago, including the listed tests. Estimates include implementation and feature testing; review/planning time is reserved separately.

| ID | Owner | PR due | Feature | Hours |
| --- | --- | --- | --- | --- |
| G01 | Ryan | Nov 04 | Application and CI foundation | 8 |
| G02 | Ryan | Nov 04 | Domain types and mock repository | 4 |
| G03 | Ibrahim | Nov 05 | Garage shell and truck overview | 8 |
| G04 | Ibrahim | Nov 10 | Add and edit truck forms | 6 |
| G05 | Ryan | Nov 11 | Mileage validation and history rules | 6 |
| G06 | Ibrahim | Nov 12 | Mileage update flow | 5 |
| G07 | Ryan | Nov 17 | Service record rules and write contract | 8 |
| G08 | Ibrahim | Nov 18 | Maintenance entry and correction forms | 6 |
| G09 | Ibrahim | Nov 19 | History and component detail pages | 4 |
| G10 | Ryan | Nov 24 | Maintenance plans and timing engine | 6 |
| G11 | Ibrahim | Nov 24 | Component cards and sort controls | 6 |
| G12 | Ryan | Dec 01 | Development auth database and API shell | 7 |
| G13 | Ryan | Dec 02 | Persistent truck and reading endpoints | 5 |
| G14 | Ibrahim | Dec 03 | Sign in and truck API adapter | 8 |
| G15 | Ryan | Dec 08 | Persistent service and plan endpoints | 8 |
| G16 | Ibrahim | Dec 09 | Connect maintenance and timing screens | 6 |
| G17 | Ibrahim | Dec 10 | Repeatable browser acceptance tests | 5 |
| G18 | Ryan | Dec 15 | Release checks and access audit | 6 |
| G19 | Ibrahim | Dec 16 | Recommendation list and component links | 5 |
| G20 | Ibrahim | Dec 17 | Mobile accessibility and interface polish | 4 |
| G21 | Ryan | Dec 22 | Final acceptance and release record | 4 |
| G22 | Ibrahim | Dec 22 | Fixes setup guide and demonstration | 4 |

Initial status for all 22 assignments is Backlog. Ownership and dates are proposed for kickoff confirmation. Detailed requirements, dependencies and acceptance tests follow on the weekly pages.

## How we work together

Use a single repo with main and short-lived feature branches. Each person clones it once, updates main before the next task, creates a feature branch, commits changes, pushes the branch and opens a PR into main. No dev branch is needed initially.

### Issue fields

Create one GitHub Issue per G-number. Include the owner, reviewer, milestone, PR deadline, estimate, dependencies, build requirements, acceptance tests, preview link and current blockers. Use Backlog, Ready, In progress, In review, Blocked and Done statuses.

### Weekly rhythm

Monday: a 20-minute planning session to confirm the week, contracts and availability. Midweek: an asynchronous update with done, next and blocked. Thursday: normal-week PR cutoff. Friday: a 30-minute preview demonstration and acceptance decision. Holiday weeks use Tuesday PR cutoffs and Wednesday gates.

### Review turnaround

Aim to respond within one working day. Raise a blocker the same day; after 30 to 60 minutes without progress, share the error, what was tried and a minimal reproduction. Open a draft PR for early help. The existing PR updates when fixes are pushed.

### PR checklist

Link the G-number/issue; explain behavior and important decisions; include screenshots for UI; list exact commands and results; attach a preview URL and note whether it uses mocks, shared staging or a local API; state known limitations. Review staged files before committing; do not include environment files or credentials.

### Merge policy

Ryan has merge authority for Ibrahim changes. Ryan changes still receive a PR, green checks and a documented review; Ibrahim can review the interface behavior, with additional technical review for security-sensitive changes when available. Choose reviewer requirements that allow documented review of Ryan backend PRs without a self-approval deadlock.

At setup, configure main to require PRs and the actual CI checks. Use review requirements that fit the two-person team and the available GitHub plan; any exception must be recorded. Disable force pushes and branch deletion where supported. This is a proposed policy, not a claim that these protections already exist.

### Definition of done

Requirements and listed tests pass; CI is green for the exact PR commit; code has been reviewed; relevant preview/staging behavior is verified; setup/contract changes are documented; the PR is merged; and the shared development deployment is smoke-tested. A feature is not Done merely because it works on one laptop.

## Development environments and delivery

| Environment | Purpose | Data and access |
| --- | --- | --- |
| Local | Each contributor builds and tests | Mocks first; disposable local test backend/database later. |
| PR preview | Review an individual frontend branch | Garage-only Vercel project. Explicit mock mode or compatible development API. |
| Shared staging | Review merged main end to end | Separate Vercel project deployment, Render API and Garage development database/auth. |
| RRC production | Existing marketplace | Outside this plan; no shared credentials, database or deployment targets. |

### One pipeline per repo

CI means automated checks; CD means deploying a checked revision. Contributors do not build their own separate deployment systems for each PR. Ryan configures the shared workflows; both contributors use them and maintain the tests affected by their changes.

### Frontend delivery

Use Vercel Git integration for branch previews. The Garage project main deployment is shared staging even if Vercel calls that environment Production. It must never point at the existing RRC project. Previews may build before CI finishes; a successful preview is not approval to merge. Validate contributor deployment permissions and applicable plan terms in G01.

### Backend delivery

Introduce one dedicated Garage Render web service in Week 5, sourced from backend/. Track main through the connected Git provider. Use After CI Checks Pass after main CI exists; require a non-skipped backend test job for backend changes. Do not automatically deploy every contributor branch to the shared API. [1]

### Frontend and backend compatibility

A UI-only preview may use the compatible shared API. A PR changing both contracts must be tested against its matching local backend or a temporary isolated backend approved by Ryan. Do not repoint the shared API at unmerged branches. Merge additive backend changes before a UI that requires them; record both deployed commit IDs.

### Database and secrets

Use a new development database/auth project with fictional data and user-scoped access. Keep elevated credentials on the server/admin path only. No privileged key goes into VITE variables or browser bundles. Never treat a hidden button as authorization. Database migrations are reviewed and tested on disposable data before staging.

### Deployment verification

CI tests run in disposable environments, not against shared staging. After deployment, verify the exact revisions, API readiness, allowed frontend origins and the main user flow. A deploy trigger is not proof the service is live. Record any hosting cost before provisioning; this document does not authorize a purchase.

## Data and behavior contracts

| Concept | Contract |
| --- | --- |
| Truck | Owner, stable ID, year/make/model/engine; optional nickname, VIN and transmission. |
| Reading | Truck, recorded date, mileage, optional engine hours; corrections retain who/when/why. |
| Component | Truck, category, name and optional physical position. |
| Service event and item | One visit with multiple actions; items reference components and service action keys. |
| Maintenance plan | Service action, baseline/next target or interval, required readings, soon windows and source metadata. |
| Recommendation | Truck, optional component, author/source, date, priority and text; demo content is labeled. |

### Required fields and units

Use miles, engine hours, ISO date-only service/reading dates and UTC audit timestamps. G02 defines exact field names and numeric precision; frontend and backend share test cases. Validate finite nonnegative numbers, configured year bounds and optional VINs. Blank optional values are absent, not misleading zeroes.

### Matching service baselines

Plans refer to a service action such as engine oil change or DPF cleaning, not just the engine/aftertreatment component. A turbo replacement cannot reset oil timing. Adding old history must not replace a newer baseline. Corrections update derived values and retain a revision trail.

### Timing precedence

Evaluate only declared plan rules. If any known target has been reached, status is Due; otherwise any known soon threshold yields Due soon. If required inputs are missing, use Unknown before Not due. Show missing-input and stale-reading hints even when a known rule is already due. Text labels express timing, never an assurance of mechanical safety.

Due is inclusive: current reading/date at or beyond the target. Due soon windows are explicit plan configuration, with clearly labeled demo values. Missing baselines remain Unknown unless an explicit target can be evaluated. For miles-remaining sorting, put items without a mileage target last and use a stable ID tie-breaker.

### Sources

Manufacturer plans require an applicable document/reference; expert advice requires author and date; owner intervals identify the owner; RRC estimates identify their basis. No real OEM schedule database or inference is being built. Do not import algorithm-generated requirements as manufacturer instructions.

### Access boundary

In Weeks 1 to 4, mock mode uses fictional data only. From Week 5, each development account can access only its own Garage records. The server verifies identity and ownership; RLS protects exposed database tables. No expert browsing or real review access is implemented in this release. [2]

## Testing and acceptance rules

Each task owner writes the tests relevant to the change. Ryan checks evidence, not just a verbal claim that it works. Required tests must run and assert behavior; empty suites, skipped jobs and retries that hide a failure do not satisfy a gate.

| Layer | Required evidence |
| --- | --- |
| Domain unit tests | Fixed clock; numeric boundaries; missing readings; matching service baselines; source validation; deterministic sorting. |
| UI behavior tests | Required input, cancel, failed save, double submission, loading/empty/error states and accessible names. |
| API and database | Validation parity, transactional writes, retry deduplication, persistence, revisions and owner-scoped relationships. |
| Access tests | Accounts A and B plus anonymous/expired sessions; direct API and direct database-user-token read/write denials. |
| Browser tests | Create truck, record mileage, log a multi-item visit, inspect status/history and refresh; isolated test data. |
| Manual review | Real phone browser plus desktop; keyboard/focus; deep links; no overflow; clear source and unknown-state wording. |
| Deployment smoke | Exact frontend/backend SHAs, readiness, CORS, sign-in, one saved record and reload. |

### CI required as work grows

Week 1: lockfile install, lint, TypeScript, meaningful unit/UI tests and frontend build. Week 5: add Python lint, backend tests, database migrations and ownership tests in disposable infrastructure. Week 6: add the complete browser flow. Run checks on PRs and main so deployment gates can evaluate merged commits.

### Failure policy

A data leak, corrupt/partial save, duplicate service records or broken core flow blocks its milestone. Minor visual issues may move to a named follow-up only if Ryan accepts them. Do not lower a passing threshold to make the schedule appear green.

### Gate record

For each week record date, gate result Pass/Fail, PR links, frontend/backend revisions, preview URL, test command/results, manual scenarios, open defects, Ryan acceptance and next action. A conditional note cannot silently mark an unmet dependency as complete.

### Scope control

At each gate compare remaining hours with availability. Drop the optional report preview first, then optional visual polish. Keep persistence, ownership, transaction integrity and required acceptance tests. If those cannot fit, move the final acceptance date and document the reason.

## Week 1 Foundation and shared contracts

Nov 2 to Nov 8 2026 | Gate Friday November 06 at 6 PM America Chicago

Demonstration: Both contributors run the same application and open the sample Cascadia dashboard from a Vercel preview.

### G01 Application and CI foundation

Owner Ryan | PR due Nov 04 | Estimate 8 hours | Depends on none

**Build.** Scaffold React, TypeScript, Vite and Tailwind; add routing, a committed lockfile, documented runtime versions, npm scripts and frontend CI. Create one separate Garage Vercel project with PR previews and a main deployment used only for development.

**Acceptance and testing.** A clean clone installs and builds using the README. A broken type or failing test makes CI fail; a nested route survives a browser refresh. Confirm both contributors can produce a preview, using a paid team setup if current account terms require it.

### G02 Domain types and mock repository

Owner Ryan | PR due Nov 04 | Estimate 4 hours | Depends on G01

**Build.** Define truck, reading, component, service event/item, plan and recommendation contracts. Provide asynchronous list/get/create/update operations and a replaceable in-memory adapter. Seed the Cascadia, another truck and missing-history examples.

**Acceptance and testing.** Contract tests create and retrieve a record, return a clear missing-ID error and isolate records by truck. Fixture validation catches a missing recommendation source. No UI component imports fixtures directly.

### G03 Garage shell and truck overview

Owner Ibrahim | PR due Nov 05 | Estimate 8 hours | Depends on G01, G02

**Build.** Build navigation, truck selection and the overview card using shared types and hooks. Show year/make/model, engine, mileage, reading date and a bundled placeholder image; include callbacks for edit and mileage actions.

**Acceptance and testing.** Render two trucks and switch between them without mixing data. Verify missing image/optional fields, loading, error and empty states. At 375px and 1440px widths the page has no horizontal overflow; buttons have accessible names.

### Milestone acceptance

Clean-clone setup, CI failure demonstration, successful preview, working truck selection and agreed type/API contracts are recorded. Ryan signs off before truck-management integration.

Review evidence: task PRs, test results and a recorded preview/staging demonstration. Ryan records Pass or Fail.

## Week 2 Truck management and mileage

Nov 9 to Nov 15 2026 | Gate Friday November 13 at 6 PM America Chicago

Demonstration: Add a truck, edit it, update its mileage and switch away and back without losing the in-session changes.

### G04 Add and edit truck forms

Owner Ibrahim | PR due Nov 10 | Estimate 6 hours | Depends on G03

**Build.** Build forms for year, make, model, engine and optional nickname, transmission and VIN. Required fields are explicit. Connect create/update actions through the repository, with clear save, cancel and error behavior.

**Acceptance and testing.** Check blank/whitespace fields, configured year bounds, optional VIN validation and cancelled edits. A failed save preserves input; a double click does not create duplicate trucks. A new truck has an honest empty history.

### G05 Mileage validation and history rules

Owner Ryan | PR due Nov 11 | Estimate 6 hours | Depends on G02

**Build.** Implement dated mileage and optional engine-hour readings. Derive current values from the latest valid reading, not whichever entry was saved last. Reject negative/nonfinite values and future dates. Require a reason for a correction that lowers a reading.

**Acceptance and testing.** Test zero, decimals according to the agreed unit policy, out-of-order readings, same-date ties, a lower reading and an explicit correction. Correction history remains attributable; a historical service entry does not replace current mileage.

### G06 Mileage update flow

Owner Ibrahim | PR due Nov 12 | Estimate 5 hours | Depends on G04, G05

**Build.** Build the mileage form and history display. Use the shared validator and repository action; show field-specific errors, saving state and correction confirmation. Display when the current reading was taken.

**Acceptance and testing.** An accepted update changes the overview and derived mileage values. A rejected update changes nothing. Test keyboard operation, cancel, failed save/retry and lower-reading confirmation. Show the temporary-data notice while using mocks.

### Milestone acceptance

Truck create/edit and mileage scenarios pass on the preview. Ryan verifies corrections preserve history and signs off the shared validation rules.

Review evidence: task PRs, test results and a recorded preview/staging demonstration. Ryan records Pass or Fail.

## Week 3 Maintenance records and history

Nov 16 to Nov 22 2026 | Gate Friday November 20 at 6 PM America Chicago

Demonstration: Record one shop visit containing oil and filter work; both items appear under the right truck and component.

### G07 Service record rules and write contract

Owner Ryan | PR due Nov 17 | Estimate 8 hours | Depends on G02, G05

**Build.** Define one maintenance event with multiple component/service items, date, mileage, optional hours, shop, cost, part brand/number and notes. Keep service action identifiers separate from component identifiers. Implement mock create/edit operations with all-or-nothing validation.

**Acceptance and testing.** Test two valid items, one invalid item, wrong-truck component IDs, historical dates, impossible readings and negative cost. A failed multi-item save writes nothing. Correcting a service keeps a revision trail and recomputes the relevant baseline.

### G08 Maintenance entry and correction forms

Owner Ibrahim | PR due Nov 18 | Estimate 6 hours | Depends on G07

**Build.** Build Add Maintenance with add/remove item rows and optional fields. Make required dates, mileage and service actions clear. Connect edits to a correction reason; preserve entries while saving or showing an error.

**Acceptance and testing.** Test multiple rows, remove/cancel, missing component/service, invalid price and double submission. One valid shop visit produces one event with multiple items. A save failure retains all fields and creates no partial history.

### G09 History and component detail pages

Owner Ibrahim | PR due Nov 19 | Estimate 4 hours | Depends on G08

**Build.** Implement truck history and component detail routes with date ordering, text/category filters and links between event and component. Display optional shop, price, parts and notes without empty labels.

**Acceptance and testing.** Verify only the selected truck appears; equal-date ordering is deterministic. Filtered-empty and completely-empty states differ. Correcting a record updates both views; route refresh and browser back work.

### Milestone acceptance

A multi-item visit, rejected partial save and corrected record are demonstrated. Ryan confirms only matching service actions reset their maintenance baselines.

Review evidence: task PRs, test results and a recorded preview/staging demonstration. Ryan records Pass or Fail.

## Week 4 Maintenance timing and attention sorting

Nov 23 to Nov 29 2026 | Gate Wednesday November 25 at 6 PM America Chicago

Demonstration: A fixed set of demo readings produces predictable due, due-soon, not-due and unknown cards.

### G10 Maintenance plans and timing engine

Owner Ryan | PR due Nov 24 | Estimate 6 hours | Depends on G07

**Build.** Implement owner-editable intervals/next targets with mandatory source metadata. Evaluate mileage, calendar date and engine hours against matching service baselines. Return due when a target is reached; keep missing information visible. Use the timing contract in this plan.

**Acceptance and testing.** Use a fixed clock to test exactly at a target, one unit before/after, leap dates and configured soon windows. A known exceeded rule wins over missing data; missing required inputs prevent an unsupported not-due result. Unrelated repairs never reset an oil baseline.

### G11 Component cards and sort controls

Owner Ibrahim | PR due Nov 24 | Estimate 6 hours | Depends on G09, G10

**Build.** Build cards showing last matching service, elapsed/remaining values, next target and source. Add attention-first, miles-remaining, recent-service and name sorting plus category filters. Build the layout against fixed status fixtures before the engine is ready.

**Acceptance and testing.** Check deterministic ties, unknown targets, empty filters and stale-reading labels. The default view puts due items first. Date/hour-only plans do not invent miles remaining, and status is conveyed in text as well as color.

### Milestone acceptance

Ryan checks expected outputs against the fixed status table. Demonstrate source labels and a missing-history truck. Thanksgiving week ends with the Wednesday gate; do not add scope.

Review evidence: task PRs, test results and a recorded preview/staging demonstration. Ryan records Pass or Fail.

## Week 5 Isolated backend and persistent truck data

Nov 30 to Dec 6 2026 | Gate Friday December 04 at 6 PM America Chicago

Demonstration: Two development accounts sign in; each sees only its own trucks and mileage after a refresh.

### G12 Development auth database and API shell

Owner Ryan | PR due Dec 01 | Estimate 7 hours | Depends on G04, G07, G10

**Build.** Create a separate Garage development database/auth project and FastAPI backend under backend/. Add reviewed migrations, seed/reset instructions, JWT verification, user-scoped database access and a readiness endpoint. Use two invite-only test accounts; no public registration flow.

**Acceptance and testing.** Rebuild an empty disposable database from migrations. Reject missing/invalid/expired tokens and a spoofed owner ID. Verify RLS with user tokens directly as well as through FastAPI. Public/exposed tables must not permit anonymous Garage access.

### G13 Persistent truck and reading endpoints

Owner Ryan | PR due Dec 02 | Estimate 5 hours | Depends on G12, G05

**Build.** Implement list/get/create/update truck and reading-history endpoints with consistent JSON/errors. Enforce ownership on the server and database. Keep responses compatible with the mock contracts; add conflict handling for simultaneous corrections.

**Acceptance and testing.** Account B cannot list, read, edit or add readings to Account A trucks, including guessed IDs and altered payloads. Invalid input is rejected consistently. Data survives an API restart; a stale edit returns a recoverable conflict.

### G14 Sign in and truck API adapter

Owner Ibrahim | PR due Dec 03 | Estimate 8 hours | Depends on G13, G06

**Build.** Build minimal test-account sign-in/sign-out and replace truck/reading mocks with the API adapter. Centralize token handling, loading and errors. Keep a separate explicit mock mode for UI work; never silently fall back after an API failure.

**Acceptance and testing.** Sign in, create a truck, update mileage, refresh and sign out. Re-login restores data; another account sees none of it. Expired sessions lead to sign-in without exposing cached account data. An unavailable API shows an actionable error.

### Milestone acceptance

Gate cannot pass on mocks. Ryan records two-account read/write isolation tests, successful migrations and persistent truck/mileage flows. Actual credentials remain outside the repo.

Review evidence: task PRs, test results and a recorded preview/staging demonstration. Ryan records Pass or Fail.

## Week 6 Persistent maintenance and complete user flow

Dec 7 to Dec 13 2026 | Gate Friday December 11 at 6 PM America Chicago

Demonstration: Sign in, create a truck, log a multi-item service, update mileage and verify the correct statuses after refresh.

### G15 Persistent service and plan endpoints

Owner Ryan | PR due Dec 08 | Estimate 8 hours | Depends on G12, G13, G07, G10

**Build.** Implement service-event/item and plan APIs with transactional saves, ownership checks and revision metadata. Make duplicate submissions safe through a request key or equivalent deduplication. Port shared validation cases to server-side tests.

**Acceptance and testing.** Force an item insert failure and confirm the whole visit rolls back. Retry a timed-out request and confirm only one event exists. Cross-owner/nested foreign IDs, invalid source attribution and stale edits are rejected. A service correction updates the right baseline.

### G16 Connect maintenance and timing screens

Owner Ibrahim | PR due Dec 09 | Estimate 6 hours | Depends on G15, G08, G09, G11, G14

**Build.** Connect all maintenance, plan and history views through the real adapter. Provide a small owner interval/next-target editor; preserve attribution and use server responses as the saved state. Refresh related queries after successful writes.

**Acceptance and testing.** Save and correct a visit, edit a custom plan and reload both truck and component routes. The summary, cards and history agree. Test timeout, validation and conflict errors; a rejected edit does not leave the dashboard showing unsaved values.

### G17 Repeatable browser acceptance tests

Owner Ibrahim | PR due Dec 10 | Estimate 5 hours | Depends on G16

**Build.** Automate the main truck-to-maintenance flow against a disposable local test backend/database. Use isolated test accounts and deterministic dates. Add a CI job with failing assertions that fail the workflow; do not mutate the shared staging database.

**Acceptance and testing.** Run the flow twice without leftover state or duplicate records. Include a failed save and refresh check. Capture useful screenshots/traces with test-only accounts and scrub tokens; manual phone testing remains required.

### Milestone acceptance

The complete persistent flow passes automated browser tests and a manual staging run. Ryan verifies no network request targets RRC production.

Review evidence: task PRs, test results and a recorded preview/staging demonstration. Ryan records Pass or Fail.

## Week 7 Recommendations and release hardening

Dec 14 to Dec 20 2026 | Gate Friday December 18 at 6 PM America Chicago

Demonstration: The development site shows attributed demo recommendations, accessible maintenance screens and a verified frontend/backend version pair.

### G18 Release checks and access audit

Owner Ryan | PR due Dec 15 | Estimate 6 hours | Depends on G15, G17

**Build.** Finish the scoped recommendations read endpoint, audit ownership for every nested route, and verify CI-gated Render deployment plus CORS. Record deployment SHAs and test a staging rollback/runbook. Keep migrations backward-compatible across frontend/backend deploys.

**Acceptance and testing.** Rerun the two-account matrix on trucks, readings, events, items, plans and recommendations. Test allowed/disallowed browser origins, unauthorized direct API access and a failed build. Verify the prior application build remains compatible with current schema; code rollback does not undo data migrations.

### G19 Recommendation list and component links

Owner Ibrahim | PR due Dec 16 | Estimate 5 hours | Depends on G18, G11

**Build.** Display fixture-backed recommendations served by the development API, with author/source, date, priority and component link. Mark all expert examples as fictional. Include a read-only sample report layout only if core work is complete.

**Acceptance and testing.** Verify truck/component association, missing-author handling, long text, empty lists and date ordering. A fabricated expert name is never displayed as a verified real expert; there is no working paid-review or expert-access action.

### G20 Mobile accessibility and interface polish

Owner Ibrahim | PR due Dec 17 | Estimate 4 hours | Depends on G16, G19

**Build.** Review the five routes and forms at 375px and 1440px. Fix keyboard/focus behavior, labels, error announcements and touch usability. Confirm plan/source language and unknown states remain clear.

**Acceptance and testing.** Complete the flow on an actual phone browser and desktop. Test keyboard-only dialogs, closing focus return, long labels, large mileage values and empty/error states. Record the tested browser/device and screenshots in the PR.

### Milestone acceptance

Feature freeze after acceptance. No unresolved data-loss, ownership or core-flow defect. Optional report polish is dropped before any required test is dropped.

Review evidence: task PRs, test results and a recorded preview/staging demonstration. Ryan records Pass or Fail.

## Week 8 Acceptance fixes and handoff

Dec 21 to Dec 27 2026 | Gate Wednesday December 23 at 6 PM America Chicago

Demonstration: Both contributors can demonstrate the isolated Garage and reproduce its setup and deployment from the written instructions.

### G21 Final acceptance and release record

Owner Ryan | PR due Dec 22 | Estimate 4 hours | Depends on G18, G20

**Build.** Run the release checklist against one recorded frontend/backend commit pair. Classify remaining defects, approve the development milestone and create a release tag only after passing. Record staging URLs, known limits and integration follow-ups.

**Acceptance and testing.** Repeat the full owner flow and two-account denial checks after deployment. Verify the actual live commit IDs and test data boundaries. A failed critical check blocks acceptance; the calendar deadline cannot override it.

### G22 Fixes setup guide and demonstration

Owner Ibrahim | PR due Dec 22 | Estimate 4 hours | Depends on G17, G20

**Build.** Resolve accepted UI defects, update setup/test instructions and prepare a short demo walkthrough. Document supported fields, reset behavior, limitations and the next backlog. Avoid introducing new features this week.

**Acceptance and testing.** From a clean checkout, follow the instructions and run the required checks. Demonstrate create/edit truck, mileage, multi-item maintenance, status, recommendations and reload. Confirm a new contributor can locate contracts, fixtures and the API adapter.

### Milestone acceptance

Final acceptance is due Wednesday Dec 23, ahead of Christmas. Ryan signs off only with evidence; Dec 24 to Dec 27 remains uncommitted contingency or time off.

Review evidence: task PRs, test results and a recorded preview/staging demonstration. Ryan records Pass or Fail.

## Release acceptance and next actions

### Eight week acceptance scenario

Using Account A on the development site, add a truck, edit its details, record a mileage reading, create a two-item service visit, set an owner maintenance plan and inspect the resulting component status. Correct the visit, reload the page and confirm overview, component and history agree. View a clearly fictional recommendation linked to that truck.

### Access and recovery scenario

Use Account B and anonymous/expired sessions to attempt access through the UI, direct API and exposed database endpoints. Ownership denials must hold for reads and writes, including altered nested component IDs. Trigger a failed service save and safe retry; confirm no partial or duplicate visit. Verify one compatible application rollback on staging without assuming database state rolls back.

### Release record

Record the repository tag, frontend/backend commit IDs, staging URLs, test results, known limits, migration version and setup/reset instructions. Ryan is accountable for the final acceptance; Ibrahim demonstrates the interface and documents its operation. No release in this plan changes www.rigrepairconnect.com.

### First actions at kickoff

Confirm the proposed November 2 start and each person's hours. Put these 22 feature cards into GitHub Issues with their G-numbers, owners and deadlines. Enable a simple board and merge/check policy. Start G01 and G02; Ibrahim can sketch G03 against the agreed contract while setup is underway.

### Updating the plan

Treat the Markdown plan in docs/eight-week-development-plan.md as the living version after merge. Update status, dates and scope through a documentation PR. This Word copy is a shareable snapshot. GitHub issues/board setup, resource provisioning and application implementation are future tasks, not actions already completed by this document.

### Platform references

Checked October 27 2026. These references support platform behavior; the feature scope, assignments and estimates are project proposals.

[1] Render deployment controls and health checks: https://render.com/docs/deploys and https://render.com/docs/health-checks

[2] Supabase row level security: https://supabase.com/docs/guides/database/postgres/row-level-security

Vercel branch previews and deployment permissions: https://vercel.com/docs/git

GitHub branch and PR workflow: https://docs.github.com/en/get-started/using-github/github-flow
