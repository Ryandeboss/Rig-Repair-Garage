# My Rig Project Brief

Rig Repair Connect  |  Ryan and Ibrahim  |  October 27 2026

## 1 What we are building

My Rig is a digital garage for heavy-duty truck owners. A driver saves their truck, records maintenance and mileage, and sees what needs attention. Useful advice stays with the truck so the next expert has better context. It will eventually live inside Rig Repair Connect.

These eight main features describe the app. Hours are total feature effort; Section 3 breaks the work into smaller tickets of four to eight hours.

#### Garage and truck profiles

Estimated total 14 hours | React and TypeScript

The owner opens My Rig, chooses a truck and sees its identity and current information. The page should feel like a practical garage: a truck image above clear, useful information.

- Add/edit year, make, model, engine and optional nickname, transmission and VIN.
- Switch between trucks; show a placeholder when no photo exists.
- Provide obvious Edit truck, Update mileage and Add maintenance actions.

#### Mileage and usage log

Estimated total 11 hours | TypeScript and React

The owner records mileage and, when known, engine hours. The dashboard shows the newest reading and its date so service timing has a clear starting point.

- Keep dated readings instead of overwriting the entire history.
- Allow corrections with a reason; older entries must not replace newer readings.
- Explain invalid values and preserve the form if saving fails.

#### Maintenance records

Estimated total 14 hours | React and TypeScript

The owner logs a shop visit or repair. One visit can contain several items, such as an oil change and fuel-filter replacement.

- Record date, mileage, work performed and the affected components.
- Optional shop, cost, part brand/number, hours and notes.
- Add/remove service items and correct mistakes without losing the original history.

### The truck history and maintenance view

#### Service history and component pages

Estimated total 4 hours | React and TypeScript

An owner can look through past work or open one component to see its own history. A future expert should be able to follow what was done and when.

- Browse visits by date and filter by text or component category.
- Link each maintenance item to its truck and component.
- Show honest empty states when history is missing.

#### Maintenance plans and attention dashboard

Estimated total 12 hours | TypeScript calculations and React

Component cards turn recorded history and an explicit service plan into a useful next-step view. Owners can set their own interval or next target and sort the most urgent items first.

- Show last matching service, miles since service, next target and source.
- Use Due, Due soon, Unknown and Not due for maintenance timing.
- Sort by attention, miles remaining, recent service or name; filter by category.

A demo card might read: Engine oil / last service 798,000 mi / 14,430 mi since service / next target 823,000 mi / source Owner demo interval. The target is sample data, not a manufacturer requirement.

#### Saved data and development accounts

Estimated total 34 hours | FastAPI Python and separate Supabase PostgreSQL Auth

After the screens work with sample data, test users sign in and save their own Garage. A refresh or server restart should not erase their trucks or services.

- Save trucks, readings, visits, service items and custom plans.
- Keep each account's records private; enforce ownership on the server/database.
- Save a multi-item visit together and make retries safe against duplicate records.

A matching service resets its own timing. Replacing a turbo does not reset engine-oil history. Missing information must stay visible rather than producing a reassuring status.

### Recommendations and the experience we want

#### Expert recommendation cards

Estimated total 5 hours | React with a read API

Advice appears beside the relevant truck or component, with enough context to understand who said it and when. The first release uses clearly fictional examples to prove the layout and links.

- Display recommendation text, date, author/source and priority.
- Open the related component and its service history.
- Keep manufacturer, expert, owner and RRC-estimate sources distinct.

#### Phone friendly screens

Estimated total 4 hours | Responsive React and Tailwind

A truck owner should be able to use the Garage on a phone without struggling through a desktop layout. Forms, cards and errors should be readable and easy to operate.

- Clear labels, touch-friendly buttons and no sideways scrolling.
- Keyboard support and sensible focus when dialogs open or close.
- Useful loading, empty and failed-save states across the five main screens.

#### Technology and development setup

| Part | What we will use |
| --- | --- |
| Screens | React, TypeScript, Vite and Tailwind; branch previews on a separate Garage Vercel project. |
| Data first | Fictional sample data behind shared load/save functions, so screens can be built early. |
| Data later | FastAPI on a separate Garage Render service; a new development Supabase database/auth project. |
| Team workflow | One GitHub repo, feature branches, reviewed PRs and shared automated checks. |

#### The eight week finish line

A test owner can add a truck, record mileage and service, set a plan, refresh and see the saved history and correct timing. Another account cannot access that data. Recommendations remain demo content. Maintenance status describes timing, not a mechanical inspection.

Paid expert reviews, live calls, payments, receipt/photo uploads, automated messages, predictive maintenance and production integration come later. Keep the Garage isolated from the live RRC marketplace.

## Building in dev mode run through

Use this routine for each weekly assignment. Branch = your work area. Commit = a saved code checkpoint. PR = a request for someone to review and merge your branch into main.

#### 1 Find your work for the week

Every Monday, open the calendar in Section 3, then read your assigned ticket below it. Check Build, Pass checks, dependencies, hours and Friday due date. Ryan confirms unclear requirements before you start. Open the matching GitHub Issue and mark it In progress.

#### 2 Open the app on your computer

Clone the repo once. After Ryan finishes the initial setup, follow the README for the agreed Node version. Run npm ci to install packages, then npm run dev. Open the local URL shown in the terminal. Before app setup exists, the repo contains documentation only.

```text
git clone https://github.com/Ryandeboss/Rig-Repair-Garage.git
cd Rig-Repair-Garage
npm ci
npm run dev
```

#### 3 Start a fresh branch

With earlier work committed and git status clean, update main and create a task branch. This example uses G03; replace it with your own ticket. Use your own GitHub account. Keep the dev server running in another terminal.

```text
git switch main
git pull --ff-only origin main
git switch -c feature/g03-truck-overview
```

#### 4 Build a small working version

Use the shared data types and load/save functions. Check the result in the local browser as you go. Stay within the ticket; ask before changing shared fields or dependencies. If stuck for 30 to 60 minutes, share the error, what you tried and your branch.

#### Where we talk and where we log work

Slack Free is enough for this two-person project: use one #rrc-garage channel with a thread for each week, plus one-to-one huddles for calls. Only 90 days of message history are accessible on the free plan, so keep requirements, decisions and test evidence in GitHub Issues/PRs. Pin the repo and this plan in the channel.

Wednesday update: Done / Next / Blocked / Hours used and remaining / Friday outlook / Branch or PR link. Post it on your issue and share the link in chat. Slack is optional; GitHub issue comments alone also work.

Slack plan reference checked October 27 2026: https://slack.com/pricing

### From local work to a reviewed change

#### 5 Run the ticket checks

Try every Pass checks item: normal use, missing/invalid input and failed saves where listed. Check UI at phone and desktop widths. Run the commands below and record actual results. Ryan creates these frontend script names during initial setup; browser tests are added later.

```text
npm run lint
npm run typecheck
npm run test:run
npm run build
```

#### 6 Commit and push your branch

Use git status and git diff to inspect changes. Stage only task files; the path below is an example. Inspect staged changes, commit and push. Never include real .env values, secrets or unrelated work.

```text
git add src/modules/garage
git diff --staged
git commit -m "G03 Add truck overview"
git push -u origin feature/g03-truck-overview
```

#### 7 Open a pull request

On GitHub choose Pull requests then New pull request. Base is main; compare is your feature branch. Link the real issue and add: what changed, how to try it, test commands/results, screenshots, preview URL and anything unfinished. G03 is our label, not necessarily GitHub issue 3. Mark a PR Draft if you still need help.

#### 8 Use the preview and fix review feedback

CI runs the shared automated checks; CD makes the test deployment. Open the Vercel preview and try the feature there. If checks fail, read the first useful error. Make fixes on the same branch, rerun checks and push again; the same PR updates. Ryan reviews and merges when ready.

#### 9 Log the finish

After merge, verify the result on shared staging. Add the merged PR, tested URL, results and approximate hours to the issue; Ryan marks Done after acceptance. Update local main before the next ticket. If you will miss Friday, flag it early with remaining work and a revised estimate.

#### Shared setup Ryan handles

Ryan configures GitHub CI, branch/review rules, Vercel previews and later the separate Render API/database. Ibrahim follows the configured workflow and maintains tests for his changes. A UI preview that needs an unmerged API must use the matching local/isolated backend. Neither person points Garage at RRC production.

If main changes while you work: from a clean feature branch run git fetch origin, then git merge origin/main. Ask Ryan for help with conflicts; do not discard or force-push to hide them. Recheck and push the updated branch.

## 3 Calendar and weekly milestones

Proposed eight weeks: November 2 to December 27 2026. Each row is one milestone. The following pages are the work tickets for those milestones. All times are Chicago time; meeting times are proposed until confirmed.

| Week | Monday plan | Wednesday update | Friday due | Milestone and tickets |
| --- | --- | --- | --- | --- |
| 1 | Nov 02 | Nov 04 | Nov 06 | Garage foundation<br>G01, G02, G03 |
| 2 | Nov 09 | Nov 11 | Nov 13 | Truck and mileage<br>G04, G05, G06 |
| 3 | Nov 16 | Nov 18 | Nov 20 | Maintenance records<br>G07, G08, G09 |
| 4 | Nov 23 | Nov 25 | Nov 27 | Service timing<br>G10, G11 |
| 5 | Nov 30 | Dec 02 | Dec 04 | Saved truck data<br>G12, G13, G14 |
| 6 | Dec 07 | Dec 09 | Dec 11 | Saved maintenance<br>G15, G16, G17 |
| 7 | Dec 14 | Dec 16 | Dec 18 | Advice and polish<br>G18, G19, G20 |
| 8 | Dec 21 | Dec 23 | Dec 25 | Final handoff<br>G21, G22 |

#### The weekly rhythm

Monday 6 PM: a 20-minute meeting to agree tasks, scope, dependencies and available hours. Wednesday by 6 PM: a short issue update showing progress, next steps and blockers. Friday by 6 PM: tested, reviewed work is merged and shown on staging; Ryan records accepted or incomplete.

Open ready-for-review PRs by Thursday noon so review is part of the deadline. Send smaller prerequisite PRs earlier. During the Thanksgiving and Christmas weeks, aim to finish by Wednesday and use a short written Friday handoff; the official deadline stays Friday November 27 and Friday December 25.

#### Effort and space for fixes

Budget 14 hours each in normal weeks and 8 each in holiday weeks. Tickets total 129 hours: Ryan 62 and Ibrahim 67. Of 200 team hours, reserve 28 for planning/review and 43 for learning, integration and fixes. Ticket estimates include testing.

#### How to use the tickets

Ryan copies tickets into GitHub Issues with owners, dates and dependency links. Needs means earlier work is required for integration; screens may start against agreed mocks. Done requires passing checks, review, merge and staging verification.

Data loss, access leaks or broken core flows block acceptance. Record unfinished work with an owner/new date; keep required tests.

### Work tickets Weeks 1 and 2

#### Week 1 due Friday November 06

##### G01 App setup and shared checks

Ryan  |  8h  |  Due Nov 06  |  Needs none

**Build** Create the Vite/React app, routes, pinned dependencies, README run commands, GitHub CI and a separate Garage Vercel project. Add the npm scripts named in Section 2.

**Pass checks** A clean clone installs/builds; a failed type/test makes CI red; deep-link refresh works; both people can open a branch preview.

##### G02 Shared types and sample data

Ryan  |  4h  |  Due Nov 06  |  Needs G01

**Build** Define truck, reading, component, service visit/item, plan and recommendation shapes. Add asynchronous mock read/write functions and two fictional trucks. Keep UI separate from storage.

**Pass checks** Create/read a record; reject missing IDs; never mix trucks; require recommendation sources. Share example inputs/outputs before G03 starts.

##### G03 Garage and truck overview

Ibrahim  |  8h  |  Due Nov 06  |  Needs G01, G02

**Build** Build the truck selector, navigation and overview card. Show identity, engine, latest mileage/date, fallback image and edit/update button callbacks using the agreed data types.

**Pass checks** Switch between two trucks; verify loading/empty/error and missing-photo states; check 375px/1440px widths and keyboard-accessible controls.

#### Week 2 due Friday November 13

##### G04 Add and edit truck

Ibrahim  |  6h  |  Due Nov 13  |  Needs G03

**Build** Build forms for year, make, model, engine and optional nickname/VIN/transmission. Save through the shared data functions; show validation, cancel and saving states.

**Pass checks** Blank required input is rejected; failed save retains input; cancel changes nothing; double-click creates only one truck; a new truck has empty history.

##### G05 Mileage rules

Ryan  |  6h  |  Due Nov 13  |  Needs G02

**Build** Store dated mileage and optional hours. Select the latest valid reading, even when older history is added later. Preserve corrections with a reason and agree numeric/date rules.

**Pass checks** Reject negative/nonfinite/future values. Test zero, same-date ties, backdated entries and lower-reading corrections. Historical service entries never overwrite current mileage.

##### G06 Mileage screen

Ibrahim  |  5h  |  Due Nov 13  |  Needs G04, G05

**Build** Build reading entry/history with the G05 rules. Show field errors and correction confirmation; update the overview from the saved result. Display the reading date.

**Pass checks** Accepted reading updates the truck; rejected/cancelled reading changes nothing. Check failed save/retry, keyboard use and visible mock-data/reset notice.

### Work tickets Weeks 3 and 4

#### Week 3 due Friday November 20

##### G07 Maintenance record rules

Ryan  |  8h  |  Due Nov 20  |  Needs G02, G05

**Build** Represent one visit with multiple service items, date/mileage and optional shop/cost/parts/notes. Match items to service actions and components; preserve correction history.

**Pass checks** Save two items together; reject wrong-truck components and invalid cost/date. One invalid item saves nothing. Corrections update only matching service baselines.

##### G08 Maintenance entry form

Ibrahim  |  6h  |  Due Nov 20  |  Needs G07

**Build** Build add/edit visit with add/remove item rows, optional fields, validation, saving state and a correction reason. Connect to the G07 write function.

**Pass checks** Check multiple items, remove/cancel, missing action/component and invalid price. Failed saves retain all rows; repeated submission creates one visit.

##### G09 History and component pages

Ibrahim  |  4h  |  Due Nov 20  |  Needs G08

**Build** Build truck history and component-detail routes, service links, date ordering and text/category filters. Display optional parts/shop/notes only when present.

**Pass checks** Only the chosen truck appears; ties sort consistently; empty/filter-empty states work; a correction updates both views; refresh and back navigation work.

#### Week 4 due Friday November 27

##### G10 Service plans and timing

Ryan  |  6h  |  Due Nov 27  |  Needs G07

**Build** Implement custom intervals or next targets with source details. Calculate timing from matching service actions using mileage/date/hours and explicit due-soon windows.

**Pass checks** Test exact target and either side, missing inputs and calendar boundaries. A known due rule wins; unknown data never becomes an unsupported Not due.

##### G11 Component cards and sorting

Ibrahim  |  6h  |  Due Nov 27  |  Needs G09, G10

**Build** Show last matching service, elapsed/remaining values, next target and source. Add category filters and attention/miles/recent/name sorting; build against fixed examples first.

**Pass checks** Due items appear first; ties stay stable; unknown targets remain clear; date/hour-only plans invent no mileage; text explains status without relying on color.

### Work tickets Weeks 5 and 6

#### Week 5 due Friday December 04

##### G12 Development accounts and database

Ryan  |  7h  |  Due Dec 04  |  Needs G04, G07, G10

**Build** Create separate Garage auth/database and FastAPI backend. Add reviewed migrations, fictional seeds, token validation, ownership policies and a readiness endpoint. Document local test setup.

**Pass checks** An empty disposable database rebuilds; invalid/expired tokens fail; anonymous and wrong-owner database/API reads/writes are denied. No production credentials are used.

##### G13 Save trucks and readings

Ryan  |  5h  |  Due Dec 04  |  Needs G12, G05

**Build** Implement owner-scoped truck and mileage endpoints matching the mock contracts. Use server validation and recoverable conflicts for stale edits; deploy the isolated API.

**Pass checks** Account B cannot read/write A trucks, including guessed IDs and spoofed owners. Data survives restart; invalid input and stale corrections return clear errors.

##### G14 Sign in and connect truck data

Ibrahim  |  8h  |  Due Dec 04  |  Needs G13, G06

**Build** Add minimal test-account sign-in/out and the API adapter for trucks/readings. Centralize session/error handling. Keep mock mode explicit; do not silently fall back after API failures.

**Pass checks** Create/update then refresh/re-login: data remains. Another account sees none of it. Expired session clears private cached data; an offline API shows a useful error.

#### Week 6 due Friday December 11

##### G15 Save maintenance and plans

Ryan  |  8h  |  Due Dec 11  |  Needs G12, G13, G07, G10

**Build** Add owner-scoped visit/item and plan APIs with transactional writes, correction history, validation and safe retry keys. Test migrations/constraints on disposable data.

**Pass checks** A forced item failure rolls back the visit; retry creates no duplicate. Reject foreign components, invalid sources and stale edits; correct only the relevant baseline.

##### G16 Connect maintenance screens

Ibrahim  |  6h  |  Due Dec 11  |  Needs G15, G08, G09, G11, G14

**Build** Connect forms, plans, cards and history to persistent APIs. Add an owner interval/next-target editor. Refresh related views after saving; use returned server values.

**Pass checks** Save/correct a visit and edit a plan, then reload: history/status agree. Failed/conflicting saves retain input and do not display unsaved values as accepted.

##### G17 Full browser test

Ibrahim  |  5h  |  Due Dec 11  |  Needs G16

**Build** Automate sign-in, truck, mileage, multi-item service, status/history and refresh against a disposable test backend. Run it in CI with isolated accounts/dates.

**Pass checks** Run twice without leftover state; include a failed save. Failures make CI red. Tests never write to shared staging; evidence contains no private tokens.

### Work tickets Weeks 7 and 8

#### Week 7 due Friday December 18

##### G18 Access and deployment checks

Ryan  |  6h  |  Due Dec 18  |  Needs G15, G17

**Build** Finish the recommendations read API. Audit all nested owner checks; verify CORS, CI-gated Render deploys and readiness. Record frontend/backend revisions and a staging recovery procedure.

**Pass checks** Recheck all record types with two accounts/anonymous access. Disallowed origins fail; bad builds do not pass. Test a compatible rollback without assuming database changes reverse.

##### G19 Recommendation cards

Ibrahim  |  5h  |  Due Dec 18  |  Needs G18, G11

**Build** Show development-API sample advice with source/author/date/priority and truck/component links. Clearly mark fictional experts. A sample read-only report is optional.

**Pass checks** Check wrong-truck links, missing author, long text, ordering and empty/error states. No demo advice appears verified and no paid-review action is active.

##### G20 Phone and keyboard polish

Ibrahim  |  4h  |  Due Dec 18  |  Needs G16, G19

**Build** Review the five screens/forms for phone layout, touch use, labels, focus handling, errors and source wording. Fix interface problems within scope.

**Pass checks** Complete the flow on a phone and desktop. Check keyboard-only dialogs/focus return, long values and 375px/1440px layouts. Attach device/browser and screenshots.

#### Week 8 due Friday December 25

##### G21 Final acceptance

Ryan  |  4h  |  Due Dec 25  |  Needs G18, G20

**Build** Run the full saved-data and two-account flows on a recorded frontend/backend revision pair. Record results, limits, staging URLs and remaining backlog; tag only after acceptance.

**Pass checks** Verify actual deployed commits, denied foreign access, no partial/duplicate saves and a reload. Any core data/access failure blocks acceptance, even on Friday.

##### G22 Fixes and handoff

Ibrahim  |  4h  |  Due Dec 25  |  Needs G17, G20

**Build** Resolve agreed UI defects; update setup/test instructions and prepare a short demonstration. Document known limits and where shared types, mocks and adapters live.

**Pass checks** A clean checkout runs using the README. Demonstrate truck/edit, mileage, service correction, status, recommendations and reload. Add no new features this week.
