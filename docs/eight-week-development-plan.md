# My Rig Team Development Handbook

Rig Repair Connect | Ryan Clark and Ibrahim | Updated October 27 2026

This handbook is the shared guide for building My Rig over eight weeks. It explains what we are building, how each person completes and records a task, and when the work is due. You do not need previous team-project experience to follow the workflow.

## 1 Features and expected results

My Rig is a digital garage inside the future Rig Repair Connect experience. Owners will add trucks, update mileage, log maintenance, see upcoming service and keep recommendations beside the relevant component. We will first build it in the separate Rig-Repair-Garage repository using fictional data, then add its own development database and API.

#### How to use the three sections

1. Section 1 describes each assignment, its owner, its dependencies and the tests that show it works. Read your assigned feature before coding.

2. Section 2 is the step-by-step working guide. Keep it open while you pick an issue, make a branch, build, test, log progress and open a pull request.

3. Section 3 is the calendar. It lists Monday planning meetings, Wednesday check-ins, Friday deadlines and estimated effort for each person.

#### What the eight week release includes

Truck list and overview; add/edit truck; mileage and optional engine hours; components; multi-item maintenance visits and corrections; maintenance history; custom service plans; attention sorting; fictional expert recommendations; phone-friendly screens; development sign-in; persistent data; automated checks and a shared test deployment.

#### Later work

Paid expert reviews, live calls, Stripe/Twilio, subscriptions, fleets, automated reminder messages, photo/receipt uploads, real manufacturer schedule imports, parts sales and production integration remain a later backlog. Truck imagery uses bundled assets. Any sample health report is optional and read-only.

#### Starting point

Repository: https://github.com/Ryandeboss/Rig-Repair-Garage. At preparation, main contains the README and the handbook is proposed in documentation PR 1. App scaffolding, issues, hosting and CI are work to complete, not systems already configured.

### Feature list at a glance

G01 to G22 are our task labels. They are not GitHub issue numbers. Each label will appear in its issue title and PR so we can follow the same work everywhere.

| ID | Owner | Assignment | Hours |
| --- | --- | --- | --- |
| G01 | Ryan | Application and CI foundation | 8 |
| G02 | Ryan | Domain types and mock repository | 4 |
| G03 | Ibrahim | Garage shell and truck overview | 8 |
| G04 | Ibrahim | Add and edit truck forms | 6 |
| G05 | Ryan | Mileage validation and history rules | 6 |
| G06 | Ibrahim | Mileage update flow | 5 |
| G07 | Ryan | Service record rules and write contract | 8 |
| G08 | Ibrahim | Maintenance entry and correction forms | 6 |
| G09 | Ibrahim | History and component detail pages | 4 |
| G10 | Ryan | Maintenance plans and timing engine | 6 |
| G11 | Ibrahim | Component cards and sort controls | 6 |
| G12 | Ryan | Development auth database and API shell | 7 |
| G13 | Ryan | Persistent truck and reading endpoints | 5 |
| G14 | Ibrahim | Sign in and truck API adapter | 8 |
| G15 | Ryan | Persistent service and plan endpoints | 8 |
| G16 | Ibrahim | Connect maintenance and timing screens | 6 |
| G17 | Ibrahim | Repeatable browser acceptance tests | 5 |
| G18 | Ryan | Release checks and access audit | 6 |
| G19 | Ibrahim | Recommendation list and component links | 5 |
| G20 | Ibrahim | Mobile accessibility and interface polish | 4 |
| G21 | Ryan | Final acceptance and release record | 4 |
| G22 | Ibrahim | Fixes setup guide and demonstration | 4 |

Hours are focused work estimates, including the listed feature tests. They are not hours per day and do not include waiting for review. Dates are in Section 3. All assignments begin in Backlog until we agree the work is ready.

### Feature descriptions G01, G02, G03

These cards explain the work. Use Section 3 for the Friday deadline and Section 2 for the GitHub process.

#### G01 Application and CI foundation

Owner Ryan | Estimate 8 hours | Needs no earlier task

**Purpose.** Give both people the same working app, test commands and preview website.

**Build.** Scaffold React, TypeScript, Vite and Tailwind; add routing, a committed lockfile, documented runtime versions, npm scripts and frontend CI. Create one separate Garage Vercel project with PR previews and a main deployment used only for development.

**Prove it works.** A clean clone installs and builds using the README. A broken type or failing test makes CI fail; a nested route survives a browser refresh. Confirm both contributors can produce a preview, using a paid team setup if current account terms require it.

#### G02 Domain types and mock repository

Owner Ryan | Estimate 4 hours | Needs G01

**Purpose.** Agree on what a truck, service and recommendation look like in code.

**Build.** Define truck, reading, component, service event/item, plan and recommendation contracts. Provide asynchronous list/get/create/update operations and a replaceable in-memory adapter. Seed the Cascadia, another truck and missing-history examples.

**Prove it works.** Contract tests create and retrieve a record, return a clear missing-ID error and isolate records by truck. Fixture validation catches a missing recommendation source. No UI component imports fixtures directly.

#### G03 Garage shell and truck overview

Owner Ibrahim | Estimate 8 hours | Needs G01, G02

**Purpose.** Let an owner choose a truck and immediately recognize its key information.

**Build.** Build navigation, truck selection and the overview card using shared types and hooks. Show year/make/model, engine, mileage, reading date and a bundled placeholder image; include callbacks for edit and mileage actions.

**Prove it works.** Render two trucks and switch between them without mixing data. Verify missing image/optional fields, loading, error and empty states. At 375px and 1440px widths the page has no horizontal overflow; buttons have accessible names.

### Feature descriptions G04, G05, G06

These cards explain the work. Use Section 3 for the Friday deadline and Section 2 for the GitHub process.

#### G04 Add and edit truck forms

Owner Ibrahim | Estimate 6 hours | Needs G03

**Purpose.** Let an owner add a truck and correct its basic details.

**Build.** Build forms for year, make, model, engine and optional nickname, transmission and VIN. Required fields are explicit. Connect create/update actions through the repository, with clear save, cancel and error behavior.

**Prove it works.** Check blank/whitespace fields, configured year bounds, optional VIN validation and cancelled edits. A failed save preserves input; a double click does not create duplicate trucks. A new truck has an honest empty history.

#### G05 Mileage validation and history rules

Owner Ryan | Estimate 6 hours | Needs G02

**Purpose.** Keep mileage history believable and avoid changing the current reading accidentally.

**Build.** Implement dated mileage and optional engine-hour readings. Derive current values from the latest valid reading, not whichever entry was saved last. Reject negative/nonfinite values and future dates. Require a reason for a correction that lowers a reading.

**Prove it works.** Test zero, decimals according to the agreed unit policy, out-of-order readings, same-date ties, a lower reading and an explicit correction. Correction history remains attributable; a historical service entry does not replace current mileage.

#### G06 Mileage update flow

Owner Ibrahim | Estimate 5 hours | Needs G04, G05

**Purpose.** Give owners a clear screen for recording mileage and viewing previous readings.

**Build.** Build the mileage form and history display. Use the shared validator and repository action; show field-specific errors, saving state and correction confirmation. Display when the current reading was taken.

**Prove it works.** An accepted update changes the overview and derived mileage values. A rejected update changes nothing. Test keyboard operation, cancel, failed save/retry and lower-reading confirmation. Show the temporary-data notice while using mocks.

### Feature descriptions G07, G08, G09

These cards explain the work. Use Section 3 for the Friday deadline and Section 2 for the GitHub process.

#### G07 Service record rules and write contract

Owner Ryan | Estimate 8 hours | Needs G02, G05

**Purpose.** Represent one shop visit accurately, even when several components were serviced.

**Build.** Define one maintenance event with multiple component/service items, date, mileage, optional hours, shop, cost, part brand/number and notes. Keep service action identifiers separate from component identifiers. Implement mock create/edit operations with all-or-nothing validation.

**Prove it works.** Test two valid items, one invalid item, wrong-truck component IDs, historical dates, impossible readings and negative cost. A failed multi-item save writes nothing. Correcting a service keeps a revision trail and recomputes the relevant baseline.

#### G08 Maintenance entry and correction forms

Owner Ibrahim | Estimate 6 hours | Needs G07

**Purpose.** Let an owner enter and correct a maintenance visit without losing their work.

**Build.** Build Add Maintenance with add/remove item rows and optional fields. Make required dates, mileage and service actions clear. Connect edits to a correction reason; preserve entries while saving or showing an error.

**Prove it works.** Test multiple rows, remove/cancel, missing component/service, invalid price and double submission. One valid shop visit produces one event with multiple items. A save failure retains all fields and creates no partial history.

#### G09 History and component detail pages

Owner Ibrahim | Estimate 4 hours | Needs G08

**Purpose.** Make a truck repair history easy to browse and trace to a component.

**Build.** Implement truck history and component detail routes with date ordering, text/category filters and links between event and component. Display optional shop, price, parts and notes without empty labels.

**Prove it works.** Verify only the selected truck appears; equal-date ordering is deterministic. Filtered-empty and completely-empty states differ. Correcting a record updates both views; route refresh and browser back work.

### Feature descriptions G10, G11

These cards explain the work. Use Section 3 for the Friday deadline and Section 2 for the GitHub process.

#### G10 Maintenance plans and timing engine

Owner Ryan | Estimate 6 hours | Needs G07

**Purpose.** Calculate maintenance timing consistently from recorded service and explicit plans.

**Build.** Implement owner-editable intervals/next targets with mandatory source metadata. Evaluate mileage, calendar date and engine hours against matching service baselines. Return due when a target is reached; keep missing information visible. Use the timing contract in this plan.

**Prove it works.** Use a fixed clock to test exactly at a target, one unit before/after, leap dates and configured soon windows. A known exceeded rule wins over missing data; missing required inputs prevent an unsupported not-due result. Unrelated repairs never reset an oil baseline.

#### G11 Component cards and sort controls

Owner Ibrahim | Estimate 6 hours | Needs G09, G10

**Purpose.** Help owners find the maintenance items that need their attention first.

**Build.** Build cards showing last matching service, elapsed/remaining values, next target and source. Add attention-first, miles-remaining, recent-service and name sorting plus category filters. Build the layout against fixed status fixtures before the engine is ready.

**Prove it works.** Check deterministic ties, unknown targets, empty filters and stale-reading labels. The default view puts due items first. Date/hour-only plans do not invent miles remaining, and status is conveyed in text as well as color.

### Feature descriptions G12, G13, G14

These cards explain the work. Use Section 3 for the Friday deadline and Section 2 for the GitHub process.

#### G12 Development auth database and API shell

Owner Ryan | Estimate 7 hours | Needs G04, G07, G10

**Purpose.** Give Garage its own test accounts, database and server, separate from RRC production.

**Build.** Create a separate Garage development database/auth project and FastAPI backend under backend/. Add reviewed migrations, seed/reset instructions, JWT verification, user-scoped database access and a readiness endpoint. Use two invite-only test accounts; no public registration flow.

**Prove it works.** Rebuild an empty disposable database from migrations. Reject missing/invalid/expired tokens and a spoofed owner ID. Verify RLS with user tokens directly as well as through FastAPI. Public/exposed tables must not permit anonymous Garage access.

#### G13 Persistent truck and reading endpoints

Owner Ryan | Estimate 5 hours | Needs G12, G05

**Purpose.** Save truck and mileage data so it survives refreshes and server restarts.

**Build.** Implement list/get/create/update truck and reading-history endpoints with consistent JSON/errors. Enforce ownership on the server and database. Keep responses compatible with the mock contracts; add conflict handling for simultaneous corrections.

**Prove it works.** Account B cannot list, read, edit or add readings to Account A trucks, including guessed IDs and altered payloads. Invalid input is rejected consistently. Data survives an API restart; a stale edit returns a recoverable conflict.

#### G14 Sign in and truck API adapter

Owner Ibrahim | Estimate 8 hours | Needs G13, G06

**Purpose.** Let test users sign in and use the saved truck data through the interface.

**Build.** Build minimal test-account sign-in/sign-out and replace truck/reading mocks with the API adapter. Centralize token handling, loading and errors. Keep a separate explicit mock mode for UI work; never silently fall back after an API failure.

**Prove it works.** Sign in, create a truck, update mileage, refresh and sign out. Re-login restores data; another account sees none of it. Expired sessions lead to sign-in without exposing cached account data. An unavailable API shows an actionable error.

### Feature descriptions G15, G16, G17

These cards explain the work. Use Section 3 for the Friday deadline and Section 2 for the GitHub process.

#### G15 Persistent service and plan endpoints

Owner Ryan | Estimate 8 hours | Needs G12, G13, G07, G10

**Purpose.** Save complete maintenance visits and plans without partial or duplicate records.

**Build.** Implement service-event/item and plan APIs with transactional saves, ownership checks and revision metadata. Make duplicate submissions safe through a request key or equivalent deduplication. Port shared validation cases to server-side tests.

**Prove it works.** Force an item insert failure and confirm the whole visit rolls back. Retry a timed-out request and confirm only one event exists. Cross-owner/nested foreign IDs, invalid source attribution and stale edits are rejected. A service correction updates the right baseline.

#### G16 Connect maintenance and timing screens

Owner Ibrahim | Estimate 6 hours | Needs G15, G08, G09, G11, G14

**Purpose.** Make the dashboard and maintenance screens work with real development storage.

**Build.** Connect all maintenance, plan and history views through the real adapter. Provide a small owner interval/next-target editor; preserve attribution and use server responses as the saved state. Refresh related queries after successful writes.

**Prove it works.** Save and correct a visit, edit a custom plan and reload both truck and component routes. The summary, cards and history agree. Test timeout, validation and conflict errors; a rejected edit does not leave the dashboard showing unsaved values.

#### G17 Repeatable browser acceptance tests

Owner Ibrahim | Estimate 5 hours | Needs G16

**Purpose.** Have the computer repeat a realistic owner journey and flag regressions.

**Build.** Automate the main truck-to-maintenance flow against a disposable local test backend/database. Use isolated test accounts and deterministic dates. Add a CI job with failing assertions that fail the workflow; do not mutate the shared staging database.

**Prove it works.** Run the flow twice without leftover state or duplicate records. Include a failed save and refresh check. Capture useful screenshots/traces with test-only accounts and scrub tokens; manual phone testing remains required.

### Feature descriptions G18, G19, G20

These cards explain the work. Use Section 3 for the Friday deadline and Section 2 for the GitHub process.

#### G18 Release checks and access audit

Owner Ryan | Estimate 6 hours | Needs G15, G17

**Purpose.** Verify the completed API protects each account and can be deployed reliably.

**Build.** Finish the scoped recommendations read endpoint, audit ownership for every nested route, and verify CI-gated Render deployment plus CORS. Record deployment SHAs and test a staging rollback/runbook. Keep migrations backward-compatible across frontend/backend deploys.

**Prove it works.** Rerun the two-account matrix on trucks, readings, events, items, plans and recommendations. Test allowed/disallowed browser origins, unauthorized direct API access and a failed build. Verify the prior application build remains compatible with current schema; code rollback does not undo data migrations.

#### G19 Recommendation list and component links

Owner Ibrahim | Estimate 5 hours | Needs G18, G11

**Purpose.** Show useful sample advice attached to the correct truck and component.

**Build.** Display fixture-backed recommendations served by the development API, with author/source, date, priority and component link. Mark all expert examples as fictional. Include a read-only sample report layout only if core work is complete.

**Prove it works.** Verify truck/component association, missing-author handling, long text, empty lists and date ordering. A fabricated expert name is never displayed as a verified real expert; there is no working paid-review or expert-access action.

#### G20 Mobile accessibility and interface polish

Owner Ibrahim | Estimate 4 hours | Needs G16, G19

**Purpose.** Make the finished screens usable on phones and with a keyboard.

**Build.** Review the five routes and forms at 375px and 1440px. Fix keyboard/focus behavior, labels, error announcements and touch usability. Confirm plan/source language and unknown states remain clear.

**Prove it works.** Complete the flow on an actual phone browser and desktop. Test keyboard-only dialogs, closing focus return, long labels, large mileage values and empty/error states. Record the tested browser/device and screenshots in the PR.

### Feature descriptions G21, G22

These cards explain the work. Use Section 3 for the Friday deadline and Section 2 for the GitHub process.

#### G21 Final acceptance and release record

Owner Ryan | Estimate 4 hours | Needs G18, G20

**Purpose.** Check the complete development release and record what was accepted.

**Build.** Run the release checklist against one recorded frontend/backend commit pair. Classify remaining defects, approve the development milestone and create a release tag only after passing. Record staging URLs, known limits and integration follow-ups.

**Prove it works.** Repeat the full owner flow and two-account denial checks after deployment. Verify the actual live commit IDs and test data boundaries. A failed critical check blocks acceptance; the calendar deadline cannot override it.

#### G22 Fixes setup guide and demonstration

Owner Ibrahim | Estimate 4 hours | Needs G17, G20

**Purpose.** Fix remaining interface problems and explain how another person runs the project.

**Build.** Resolve accepted UI defects, update setup/test instructions and prepare a short demo walkthrough. Document supported fields, reset behavior, limitations and the next backlog. Avoid introducing new features this week.

**Prove it works.** From a clean checkout, follow the instructions and run the required checks. Demonstrate create/edit truck, mileage, multi-item maintenance, status, recommendations and reload. Confirm a new contributor can locate contracts, fixtures and the API adapter.

### Shared rules behind the features

These rules prevent two people from implementing the same behavior differently. Ryan writes the exact types and examples during G02. If a rule is unclear, ask in the issue before building around an assumption.

| Concept | Plain meaning |
| --- | --- |
| Truck | One owner vehicle, with a stable ID and basic identity fields. |
| Reading | Mileage and optional engine hours recorded on a particular date. |
| Component | A truck part or assembly, sometimes with a position such as left steer. |
| Service event and item | One shop visit, containing one or more maintenance actions. |
| Plan | A service interval or explicit next target, with its source recorded. |
| Recommendation | Advice with an author/source, date and optional component link. |

#### Maintenance timing is not a mechanical inspection

Use Due, Due soon, Unknown and Not due. A known reached target wins; a known approaching target comes next. Missing required readings/baselines remain Unknown before claiming Not due. Keep missing-data hints visible even when another known rule is due. Date, mileage and hour thresholds belong to the plan; demo values must be labeled.

A matching service action resets its own timing. Replacing a turbo does not reset engine-oil timing. Backdated history must not replace a newer baseline. Use miles, engine hours, date-only service dates and UTC audit timestamps; agree numeric precision and correction rules in G02.

#### Sources and privacy

Manufacturer recommendations need an applicable reference. Expert advice needs attribution and a date; samples must say fictional/demo. Owner intervals and RRC estimates have their own labels. No AI estimate may appear as a manufacturer requirement. From Week 5, both the server and database must protect account ownership; expert browsing is not part of this release.

#### Ownership and asking for help

Ryan owns architecture, shared contracts, maintenance rules, backend, security, deployments and final acceptance. Ibrahim owns the assigned screens, forms, integrations and frontend/browser tests. Both explain their code and handle review feedback. AI tools are fine; ask about anything you cannot explain or debug.

## 2 Step by step working guide

Use the same sequence for every feature: choose an assigned Ready issue, create a branch, build a small change, test it, commit and push, open a PR, respond to review, then verify the merged result. You are not expected to know the whole application before your first task.

#### The words you will see

| Term | What it means here |
| --- | --- |
| Repository or repo | The shared project files and their change history on GitHub. |
| Clone | Download the repo and its Git history to your computer once. |
| Branch | Your separate line of work, such as feature/g03-truck-overview. |
| Commit and push | Commit saves a named change locally; push uploads those commits to GitHub. |
| Issue | The task page: requirements, owner, deadline, progress and discussion. |
| Pull request or PR | A request to review your branch and combine it into main. |
| Merge | Bring an accepted branch into main. A push alone does not merge it. |
| CI | Automatic checks of the code, such as tests, types and builds. |
| CD and preview | Deployment automation; a preview is a test website for a particular branch. |
| API and staging | The API is the server interface; staging is our shared integrated test site. |
| Contract and mock | A contract is an agreed data/function shape; a mock uses fictional local data. |

#### Before your first task

Ryan invites Ibrahim to this Garage repo and confirms access. Each person uses their own GitHub login. Install Git, VS Code and the Node version Ryan records in the README. We will use the VS Code terminal for these examples. Backend tools are introduced in Week 5; Ibrahim does not need production credentials.

### Step 1 Set up your local copy

1. Accept the GitHub collaborator invitation and open the repository in your own account. Ask Ryan if you cannot see it or push a branch.

2. Open a terminal in the folder where you keep projects. Run the clone commands below once.

3. Open the downloaded folder in VS Code. Open Terminal then New Terminal. Check that the prompt is inside Rig-Repair-Garage.

4. Read the README. After G01 is merged, run the install/start commands below. Before G01 exists, only the documentation is available; do not try to fix missing npm scripts yourself.

5. Open the local URL printed by Vite. Check that the app opens without an error and tell Ryan you can run it. This is your local copy, not the shared test website.

```text
git clone https://github.com/Ryandeboss/Rig-Repair-Garage.git
cd Rig-Repair-Garage
```

#### After Ryan adds the application

```text
npm ci
npm run dev
```

npm ci installs exactly the dependencies recorded in the lockfile. npm run dev starts the local app and stays running until you press Ctrl+C. Open a second terminal for Git or testing commands. If no URL appears, copy the error into your issue rather than guessing at package upgrades.

#### Commands Ryan establishes in G01

| Command | Purpose |
| --- | --- |
| npm run dev | Start the frontend on your computer. |
| npm run lint | Check common code-quality problems. |
| npm run typecheck | Check TypeScript types. |
| npm run test:run | Run frontend unit/UI tests once. |
| npm run build | Check that the app can be built for deployment. |
| npm run test:e2e | Run full browser tests after G17 adds them. |

These script names are the required setup convention for G01/G17, not a claim that they exist today. Follow the committed README if the team later changes them. Do not add secrets to source files or commit local .env files.

### Step 2 Choose a task and record the plan

1. At Monday planning, Ryan and Ibrahim agree the week assignments in Section 3. Ryan creates one GitHub Issue for each G-number and fills its requirements from Section 1.

2. Open the repo then Issues. Find the issue assigned to you; a Project board is an optional view of the same issues. Work on one active task at a time.

3. Read Purpose, Build, Prove it works, dependencies and Friday due date. Open each dependency. If it is unfinished, ask whether you can build against its agreed mock data first.

4. Write a short comment describing your approach and any uncertainty. Ryan confirms shared types, file boundaries and expected behavior. Move the issue to In progress when you actually begin.

5. Record progress in the issue throughout the week. Update approximate hours used and remaining, plus any blocker; exact time tracking is not required. Keep design decisions in the issue so they are not lost in texts.

#### Issue fields Ryan fills in

| Field | What to enter |
| --- | --- |
| Title and owner | Example G03 Garage shell and truck overview; owner Ibrahim. |
| Due date and estimate | The week Friday at 6 PM Chicago time; estimated focused hours. |
| Requirements and tests | Copy the feature card; clarify expected inputs/results. |
| Dependencies | G01 and G02, with links to the real GitHub issues. |
| Status and evidence | Progress, branch, PR link, preview and test results. |

#### Example planning comment for G03

Plan: build TruckOverview with the agreed truck type. First show the sample truck, then add the missing-photo state and mobile layout. I need Ryan to confirm where the loading/error state lives. Estimate: 8 hours total; no work logged yet.

Use Backlog for future ideas, Ready for agreed work, In progress while building, Blocked when you cannot continue, In review once the PR is ready, and Done only after merge and staging verification. If a board is not configured, use the same words as issue labels.

### Step 3 Create a branch and build the feature

1. Start with your earlier work committed and a clean working directory. Run git status. If there are unexpected changes, ask before switching or discarding anything.

2. Switch to main and pull the latest accepted changes. Create a new branch for this task. G03 is the example below; use your own G-number and a short feature name.

3. Read the nearest existing component and the shared type before editing. Build the smallest useful part first and check it in the local browser.

4. Connect through the shared hooks/repository functions rather than importing sample JSON directly. Keep the change within the agreed issue. Ask before changing shared field names, dependencies or other contributors files.

5. Save small checkpoints as you work. You can push an unfinished branch and open a draft PR for help; mark it clearly as draft and explain what remains.

```text
git status
git switch main
git pull --ff-only origin main
git switch -c feature/g03-truck-overview
git branch --show-current
```

#### Worked example for G03

Create or update the agreed overview component under src/modules/garage/. Give it the agreed truck data through props and callbacks for the buttons. Show the year/make/model, engine, mileage and reading date. Use a bundled fallback image. Build the missing-data and narrow-screen states before polishing details.

#### What to log while you work

Example: Completed the overview text and fallback image. Next: mobile layout and component tests. About 3 hours used, 5 remaining. Blocker: none. Branch: feature/g03-truck-overview.

#### If you get stuck

After about 30 to 60 minutes without progress, post the exact error, steps to reproduce, what you tried and the relevant code/branch. Mark Blocked if you cannot continue. Do not wait until Friday. A question or early draft PR is an expected part of teamwork.

### Step 4 Test before asking for review

1. Turn each Prove it works statement into a concrete check. Write down the starting data, action, expected result and actual result.

2. Add automated tests for behavior that can break: validation, status rules, saving/cancel and the way screens respond to errors. Start with one normal case and then the listed edge cases.

3. Run lint, type checking, frontend tests and the build using the commands below. Fix failures related to your change before marking the PR ready.

4. Try the feature manually in the local browser. For UI, check 375px and 1440px widths, keyboard navigation and missing/error states. Record what you actually tested.

5. Add the results to the PR and link them in the issue. A screenshot shows appearance; it does not replace a save/validation test.

```text
npm run lint
npm run typecheck
npm run test:run
npm run build
```

#### Example test notes for G03

| Check | Action | Expected result |
| --- | --- | --- |
| Normal truck | Open sample Cascadia | Correct identity, engine, mileage and reading date. |
| Missing photo | Render truck without photo | Bundled placeholder; text remains readable. |
| Different truck | Select the second truck | Every displayed value belongs to that truck. |
| Phone layout | Use 375px viewport | No horizontal scroll; all buttons remain usable. |
| Loading or error | Simulate pending/failed load | Clear state and recovery; no misleading truck data. |

#### Backend and browser tests later

From Week 5, Ryan documents Python install/test commands and supplies a disposable test database. Backend PRs run their own validation, ownership and transaction tests. From Week 6, run the browser suite on its isolated test backend. Never run reset scripts or automated write tests against the shared staging database or RRC production.

Test output must report real executed checks. A skipped suite, empty test file, preview that merely loads, or unchanged screenshot is not evidence that the feature requirements passed.

### Step 5 Commit push and open a PR

1. Run git status and git diff to review your changes. Stage only the files belonging to the task. The example stages the Garage module; replace the path if your task changes other files.

2. Run git diff --staged. Check that no .env, credentials, unrelated files or generated build folders are included. Commit with a short description of the change.

3. Push your branch to GitHub. If Git requests authentication or identity, use your own account/name and follow the README; never use Ryan credentials.

4. Open the repo Pull requests page, choose New pull request, and compare your feature branch into main. Check the file list. Use Draft if you still need help; otherwise request Ryan review.

5. Fill the PR template under Copyable progress and review templates, link the real issue URL, and add the PR URL to the issue. Move the task to In review when it is ready.

```text
git status
git diff
git add src/modules/garage
git diff --staged
git commit -m "G03 Add truck overview card"
git push -u origin feature/g03-truck-overview
```

#### How to read the automated results

GitHub Actions runs the shared CI workflow after the push. Open the PR checks. If a check fails, open its log, find the first useful error and fix it locally. Commit and push the fix to this same branch; the existing PR updates. Do not create a replacement PR for every correction.

Vercel creates a branch preview once G01 is configured. Open it and repeat the relevant manual checks. Put the URL in the PR and state whether it uses mocks or the development API. If no preview appears, tell Ryan; a CI pass and a preview deployment are different checks.

#### Before marking ready

Check the title, linked issue, scope, exact test commands/results, screenshots, preview URL and remaining limitations. The G03 task label is not necessarily GitHub issue 3; link the actual issue that Ryan created. Do not merge your own task just because GitHub displays a green button.

### Step 6 Respond to feedback and finish

1. Ryan reads the PR and tries the feature. He may ask for a fix or explanation. Reply to each point; ask if the feedback is unclear.

2. Make changes on the same branch, rerun affected checks, commit and push. Tell the reviewer what changed. CI runs again for the new commit.

3. If main has moved, update your branch using the commands below from a clean working directory. If Git reports a conflict, stop and resolve it with Ryan; do not force-push, reset or delete files to hide it.

4. When required checks and review pass, Ryan merges the PR. The main deployment updates. Ryan and the task owner then verify the feature on shared staging.

5. Add a completion comment to the issue with the merged PR, staging URL and final test result. Ryan moves it to Done/closes it after verification. Delete the finished remote branch when agreed, then update local main before the next feature.

```text
git fetch origin
git merge origin/main
# Resolve any conflicts with Ryan before continuing.
# Rerun the relevant checks, then push the updated branch.
git push
```

#### After the PR is merged and your tree is clean

```text
git switch main
git pull --ff-only origin main
```

#### What Done means

The feature meets the card requirements, its tests ran and passed, review is complete, the PR is merged, and the matching shared development deployment was checked. A pending deploy or failing core scenario means the issue remains open. Record remaining minor limitations as separate follow-ups accepted by Ryan.

#### If you will miss Friday

Post the completed work, remaining work, reason, revised estimate and any help needed as soon as you know. Agree a smaller acceptable slice or a new date with Ryan. Keep the original deadline and changed date visible in the issue. Never mark unfinished work Done to keep the calendar green.

### Copyable progress and review templates

Use these short structures in GitHub. They are examples to copy and replace with your actual feature, results and links.

#### Wednesday check in as an issue comment

```text
Feature: G03
Done: overview text and placeholder image
Next: phone layout and component tests
Time: about 3h used; about 5h remaining
Blockers or questions: none
Friday outlook: on track
Branch or draft PR: paste link
```

#### PR description

```text
Feature and issue: G03; paste actual issue URL
What changed: describe the behavior
How to try it: route and steps
Automated checks: commands and actual results
Manual checks: device/width and scenarios
Preview URL and data mode: paste link; mock or API
Screenshots: attach relevant UI views
Known limits or questions: list them
```

#### Friday completion or carryover comment

```text
Feature: G03
Result: accepted / incomplete
PR and tested commit: paste links or SHA
Preview or staging URL: paste link
Checks and demonstration: summarize actual results
Hours used and remaining: approximate
Open defects or carryover: list with owner/date
Ryan acceptance: pending or recorded by Ryan
```

Each contributor posts their own update. Ryan records the milestone result in a weekly issue, such as Week 1 acceptance, linked to all that week task issues. These templates are not new reporting systems; the issue and PR hold the record.

### Ryan setup checklist for the shared workflow

Ryan owns this configuration. Ibrahim needs to know what the systems do, but should not have to invent the pipeline or manage private server credentials while completing a UI task.

1. During G01, add the frontend and documented npm scripts, pin the agreed runtime/dependencies and commit the lockfile. Create .github/workflows/ci.yml for PR and main checks: install, lint, types, tests and build. Confirm an intentionally failing check blocks acceptance.

2. Create the shared issue/PR templates and a simple board or labels. Configure main to require PRs and actual CI check names. Choose a review policy that works for two people: Ryan reviews Ibrahim PRs; Ryan changes also receive a PR, checks and documented review, with technical review when needed.

3. Connect a separate Garage Vercel project to this repo. Configure branch previews and the main deployment as Garage staging. Confirm both contributors can produce previews and verify account/plan requirements before paying for anything.

4. During G12/G13, add backend/ and a new Garage development database/auth project. Add migrations, fictional seeds, invite-only test accounts, verified identity and ownership checks. Document .env.example with variable names/placeholders only; never commit real values.

5. Create a separate Garage Render web service using the backend folder, documented build/start commands and an HTTP readiness endpoint. Track main via the connected Git provider; use After CI Checks Pass once main backend checks run. Keep all endpoints and credentials separate from RRC production.

6. Add disposable backend/database test jobs during Week 5 and browser CI during Week 6. Verify migrations and ownership with two accounts. Checks must actually execute on the commits being deployed, not all be skipped.

7. For each deployment, record the actual frontend/backend revisions and run the saved-data flow. Keep backward-compatible API changes so frontend and backend can deploy separately. A frontend PR that needs an unmerged backend must use a matching local or isolated backend, not replace the shared staging API.

#### What each environment is for

Local: your own app and mocks/test database. PR preview: the website for your branch. Shared staging: merged main with the development API/database. Existing RRC production: outside this project. Vercel may label the Garage main deployment Production; it is still our isolated development site.

PR previews can build before CI completes; they are for inspection, not proof of acceptance. Deployment automation is shared configuration. Contributors maintain the tests affected by their PRs, not a separate CI/CD system per feature.

## 3 Schedule and weekly calendar

Proposed kickoff is Monday November 2 2026. Week 8 ends Sunday December 27. Every official due date is Friday at 6 PM Chicago time; final acceptance is Friday December 25. Confirm availability at kickoff and update the issue dates if the team agrees a change.

| Week | Monday | Wednesday | Friday due | Features |
| --- | --- | --- | --- | --- |
| 1 | Nov 02 | Nov 04 | Nov 06 | G01, G02, G03 |
| 2 | Nov 09 | Nov 11 | Nov 13 | G04, G05, G06 |
| 3 | Nov 16 | Nov 18 | Nov 20 | G07, G08, G09 |
| 4 | Nov 23 | Nov 25 | Nov 27 | G10, G11 |
| 5 | Nov 30 | Dec 02 | Dec 04 | G12, G13, G14 |
| 6 | Dec 07 | Dec 09 | Dec 11 | G15, G16, G17 |
| 7 | Dec 14 | Dec 16 | Dec 18 | G18, G19, G20 |
| 8 | Dec 21 | Dec 23 | Dec 25 | G21, G22 |

#### Monday planning meeting

Proposed time: 6 PM Chicago, about 20 minutes. Review last Friday results, choose each person next Ready issue, clarify shared data/files, confirm available hours and identify dependencies. Ryan updates owners, scope and deadlines in GitHub. End with each person knowing their first task.

#### Wednesday check in

Post the short issue update by 6 PM Chicago: done, next, hours used/remaining, blockers and Friday outlook. Include a screenshot or draft PR when useful. Add a 10-minute call only if a blocker needs discussion; do not wait for this check-in to raise an urgent blocker.

#### Friday deadline and acceptance

By 6 PM Chicago, work should be tested, reviewed, merged and demonstrated on staging. Open a ready-for-review PR by Thursday noon to allow feedback and fixes; smaller prerequisite PRs should arrive earlier. Ryan records Pass or Fail against the weekly scenario. A failing dependency does not pass because the date arrived.

#### Holiday weeks keep their Friday deadlines

November 27 is the Friday after Thanksgiving and December 25 is Christmas. They have reduced scope. Aim for ready PRs by Tuesday and code/testing completion by Wednesday; keep Friday as the official due day with a short written handoff. If either person needs a different arrangement, agree and record it at Monday planning.

### Weekly assignments Weeks 1 to 4

All dates are 2026. Feature hours include implementation and feature-specific tests. Add the weekly planning/review allowance separately; remaining capacity is a buffer for learning, integration and fixes.

#### Week 1 due Friday November 06

Ryan: G01 Application and CI foundation (8h); G02 Domain types and mock repository (4h). Total 12h.

Ibrahim: G03 Garage shell and truck overview (8h). Total 8h.

**Friday demonstration.** Both contributors run the same application and open the sample Cascadia dashboard from a Vercel preview.

**Acceptance.** Clean-clone setup, CI failure demonstration, successful preview, working truck selection and agreed type/API contracts are recorded. Ryan signs off before truck-management integration.

#### Week 2 due Friday November 13

Ryan: G05 Mileage validation and history rules (6h). Total 6h.

Ibrahim: G04 Add and edit truck forms (6h); G06 Mileage update flow (5h). Total 11h.

**Friday demonstration.** Add a truck, edit it, update its mileage and switch away and back without losing the in-session changes.

**Acceptance.** Truck create/edit and mileage scenarios pass on the preview. Ryan verifies corrections preserve history and signs off the shared validation rules.

#### Week 3 due Friday November 20

Ryan: G07 Service record rules and write contract (8h). Total 8h.

Ibrahim: G08 Maintenance entry and correction forms (6h); G09 History and component detail pages (4h). Total 10h.

**Friday demonstration.** Record one shop visit containing oil and filter work; both items appear under the right truck and component.

**Acceptance.** A multi-item visit, rejected partial save and corrected record are demonstrated. Ryan confirms only matching service actions reset their maintenance baselines.

#### Week 4 due Friday November 27

Ryan: G10 Maintenance plans and timing engine (6h). Total 6h.

Ibrahim: G11 Component cards and sort controls (6h). Total 6h.

**Friday demonstration.** A fixed set of demo readings produces predictable due, due-soon, not-due and unknown cards.

**Acceptance.** Demonstrate the expected status outputs, source labels, unknown history and stable sorting. Aim to finish by Wednesday November 25; Friday November 27 remains the official deadline and may use a written demonstration.

### Weekly assignments Weeks 5 to 8

All dates are 2026. Feature hours include implementation and feature-specific tests. Add the weekly planning/review allowance separately; remaining capacity is a buffer for learning, integration and fixes.

#### Week 5 due Friday December 04

Ryan: G12 Development auth database and API shell (7h); G13 Persistent truck and reading endpoints (5h). Total 12h.

Ibrahim: G14 Sign in and truck API adapter (8h). Total 8h.

**Friday demonstration.** Two development accounts sign in; each sees only its own trucks and mileage after a refresh.

**Acceptance.** Gate cannot pass on mocks. Ryan records two-account read/write isolation tests, successful migrations and persistent truck/mileage flows. Actual credentials remain outside the repo.

#### Week 6 due Friday December 11

Ryan: G15 Persistent service and plan endpoints (8h). Total 8h.

Ibrahim: G16 Connect maintenance and timing screens (6h); G17 Repeatable browser acceptance tests (5h). Total 11h.

**Friday demonstration.** Sign in, create a truck, log a multi-item service, update mileage and verify the correct statuses after refresh.

**Acceptance.** The complete persistent flow passes automated browser tests and a manual staging run. Ryan verifies no network request targets RRC production.

#### Week 7 due Friday December 18

Ryan: G18 Release checks and access audit (6h). Total 6h.

Ibrahim: G19 Recommendation list and component links (5h); G20 Mobile accessibility and interface polish (4h). Total 9h.

**Friday demonstration.** The development site shows attributed demo recommendations, accessible maintenance screens and a verified frontend/backend version pair.

**Acceptance.** Feature freeze after acceptance. No unresolved data-loss, ownership or core-flow defect. Optional report polish is dropped before any required test is dropped.

#### Week 8 due Friday December 25

Ryan: G21 Final acceptance and release record (4h). Total 4h.

Ibrahim: G22 Fixes setup guide and demonstration (4h). Total 4h.

**Friday demonstration.** Both contributors can demonstrate the isolated Garage and reproduce its setup and deployment from the written instructions.

**Acceptance.** Ryan records final acceptance on Friday December 25 after checking the agreed release evidence. Aim to complete code and testing by Wednesday December 23; use a short written Friday submission if both contributors are away.

### Capacity acceptance and keeping the plan current

#### Approximate time commitment

Plan for 14 hours per person in each normal week and 8 hours per person in Weeks 4 and 8. That is 200 team hours across the eight weeks. The feature cards total 129 hours: Ryan 62 and Ibrahim 67. Allow 28 team hours for planning/review and keep roughly 43 hours for learning, integration and unexpected fixes. These estimates are a starting point; adjust them after the first real tasks.

#### How to record a Friday milestone

1. Open the weekly acceptance issue and link each feature issue and merged PR.

2. Record the preview/staging URL, actual frontend/backend commit IDs and test commands/results. Use local/mock evidence only in Weeks 1 to 4; later gates require persistent development data.

3. Run the week demonstration and record observed results, not just checkmarks.

4. Ryan records Pass or Fail, accepted minor limitations and any unfinished item with its owner/new date. Hold dependent integration if the required scenario fails.

#### Final acceptance

Account A adds/edits a truck, records mileage, saves a multi-item service and custom plan, sees correct history/status after refresh, and views a clearly fictional recommendation. Account B and anonymous/expired sessions cannot access A records through the UI, API or exposed database routes. A forced failed service save creates no partial/duplicate visit. Both people can run the project from a clean checkout and explain the deployment/setup guide.

#### If the schedule starts slipping

Drop the optional sample report and extra visual polish before dropping persistence, ownership checks or required tests. Split work into smaller PRs and update estimates. If the core scope cannot fit, Ryan changes scope or the final date openly; do not hide carryover or label unfinished work complete.

#### Where future edits go

After merge, docs/eight-week-development-plan.md is the living version of this handbook. Issues hold current progress and changed dates; documentation PRs update shared rules/scope. This Word file is the shareable snapshot. This revision changes documentation only; it does not create actual meetings, reminders, issue assignments, hosting or CI jobs.

#### Reference guides

GitHub workflow: https://docs.github.com/en/get-started/using-github/github-flow
Vercel previews: https://vercel.com/docs/git
Render deployment controls: https://render.com/docs/deploys
Render readiness checks: https://render.com/docs/health-checks
Supabase ownership policies: https://supabase.com/docs/guides/database/postgres/row-level-security
