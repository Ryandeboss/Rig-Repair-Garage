# Rig Repair Garage — My Rig

**A digital garage for truck owners, built as a new module of [Rig Repair Connect](https://www.rigrepairconnect.com).**

My Rig brings a truck's maintenance history, components, mileage, and expert recommendations into one place. The goal is to help owners understand what has been done, what needs attention, and what to discuss with a qualified heavy-duty truck expert.

**Project status:** Planning / initial setup. This repository currently documents the proposed product. The application, installation scripts, and features described below have not been implemented yet. Scope and technical details can evolve as we build.

## Why we are building this

Rig Repair Connect, operated by Apex Summit LLC, connects truck owners and owner-operators with experienced heavy-duty truck professionals for remote consultations.

My Rig extends that relationship beyond a single call. Instead of explaining the same truck history every time an issue comes up, an owner can keep a useful record that an authorized expert can review.

Over time, the product should connect these activities:

1. An owner adds a truck and its known maintenance history.
2. They update mileage and record services or repairs.
3. They request expert help when needed.
4. The expert's recommendations are saved with the relevant truck and component.
5. The owner records the outcome, giving future consultations better context.

The value comes from useful records and real expert knowledge.

## What the experience should feel like

Think of a practical, video-game-inspired garage: a truck photo or illustration at the top, with clear maintenance and component cards underneath.

The first version should be professional, easy to scan, and comfortable to use on a phone. An elaborate 3D truck is outside the initial scope.

A sample truck for development:

| Field | Demo value |
| --- | --- |
| Truck | 2019 Freightliner Cascadia |
| Engine | Detroit DD15 |
| Current mileage | 812,430 miles |
| Last engine oil service | 798,000 miles |
| Last fuel filter replacement | 780,500 miles |
| Last DPF cleaning | 705,000 miles |

These are fictional development records, not maintenance recommendations.

A component card might show its name, last service, miles since service, next service target, status, and the source of its maintenance interval.

## First MVP

The first goal is a working frontend prototype using mock data.

### Garage and truck dashboard

- View the owner's trucks.
- Add and edit a truck.
- Open a truck dashboard with its photo, basic information, and mileage.
- Record mileage updates.
- See maintenance items that need attention.

### Components and maintenance

- View components grouped into practical categories.
- Add a maintenance record with a date, mileage, work performed, and optional shop, cost, part details, and notes.
- Allow one service visit to include multiple maintenance items.
- Browse maintenance history and component-specific records.
- Sort items by attention needed, miles remaining, recent service, or component name.

### Recommendations

- Display clearly labeled mock expert recommendations.
- Link recommendations to a truck and, where relevant, a specific component.
- Preserve who or what each recommendation came from.

### MVP completion

The prototype is useful when someone can add a truck, update its mileage, record a service, and see that change reflected in its dashboard and component history.

The initial mock adapter will hold changes in temporary application state. Changes will reset on refresh until persistence is added; the interface should make this clear.

## Maintenance status and recommendation sources

Maintenance timing and physical condition are different things. Being within a service interval does not prove that a component is in good condition.

Use these maintenance timing labels:

| Status | Meaning |
| --- | --- |
| Overdue | A recorded service target has been exceeded |
| Due soon | A known target is approaching |
| Not due | Available records place the item before its service target |
| Unknown | The service history, interval, or current readings are insufficient |

Status rules should consider applicable mileage, date, and engine-hour limits. Missing information must remain visible rather than being converted into a reassuring status.

Each maintenance plan or recommendation must identify its source:

- **Manufacturer:** Relevant document or reference and applicable vehicle configuration.
- **RRC expert:** Expert identity and recommendation date.
- **Owner:** A custom interval selected by the truck owner.
- **RRC estimate:** Clearly identified as an estimate, with its basis.

All starting intervals are demonstration data. Sample expert content must be labeled as fictional. AI-generated estimates must never be presented as manufacturer requirements.

## Planned screens

| Route | Purpose |
| --- | --- |
| `/garage` | Truck list and Add Truck action |
| `/garage/trucks/:truckId` | Truck dashboard |
| `/garage/trucks/:truckId/maintenance` | Maintenance history |
| `/garage/trucks/:truckId/components/:componentId` | Component details and history |
| `/garage/trucks/:truckId/recommendations` | Recommendations for the truck |

Add Truck, Edit Truck, Update Mileage, and Add Maintenance can use dialogs or mobile sheets.

## Proposed technical approach

Use technologies compatible with the existing RRC application:

| Layer | Initial prototype | Later development |
| --- | --- | --- |
| Frontend | React, TypeScript, Vite, Tailwind CSS | Integrate the Garage module into RRC |
| Data access | Mock repository adapter | API-backed adapter |
| Backend | Not required initially | FastAPI / Python |
| Database | Not required initially | Separate development PostgreSQL / Supabase environment |

Keep three responsibilities separate:

- **Presentation:** Pages, forms, cards, and layouts.
- **Domain logic:** Data types, validation, maintenance status, and sorting.
- **Data access:** Loading and saving through a small repository interface.

UI components should use application hooks/actions rather than importing fixture data or calling database services directly. This lets us replace mock storage with real APIs while retaining the UI and business logic.

### Proposed folder structure

```text
src/
  app/                        # Application shell and routing
  modules/
    garage/
      pages/
      components/
      domain/                 # Types, validation, status calculations
      data/                   # Repository interface and adapters
      hooks/
      fixtures/               # Fictional development data
  shared/
    ui/
docs/                         # Future design and implementation notes
```

This is a proposed structure, not a list of files already present.

### Initial data concepts

- **Truck:** Vehicle identity and basic configuration.
- **Mileage reading:** Dated mileage and optional engine hours.
- **Component:** A truck component, including position where relevant.
- **Maintenance record:** A service visit or repair event.
- **Maintenance item:** Work on a component within that record.
- **Maintenance plan:** Interval or next service target, including its source.
- **Recommendation:** Attributable advice linked to a truck or component.

These concepts are a starting point, not a finalized database schema.

## Why this repository is separate

The existing RRC marketplace already handles authentication, payments, experts, and real users. Garage is being developed as its own module so we can experiment, collaborate, and validate the experience in an isolated environment.

**My Rig is intended to become part of Rig Repair Connect.** This repository is its development home, not a separate business.

For this project:

- Use fictional data initially.
- Never connect the prototype to the production RRC database.
- Never copy production Supabase service-role credentials, Stripe secrets, Twilio credentials, or private customer data into this project.
- Keep credentials out of Git.
- Use separate development services if a backend becomes necessary.
- Coordinate any future production integration with Ryan.

## Collaboration and ownership

**Ryan Clark** coordinates product direction, architecture, shared data contracts, and final integration.

A strong initial ownership area for a collaborator is **the Garage dashboard and maintenance UI**, including:

- Truck and component cards.
- Add Truck and maintenance forms.
- History and component detail screens.
- Sorting/filtering controls.
- Recommendation presentation.
- Mobile layouts, accessibility, fixtures, and frontend tests.

Ryan will lead backend security, authentication, database migrations, payments, payouts, production deployments, and integration with the existing RRC marketplace.

### Working together

1. Agree on a small task and its acceptance criteria.
2. Create a branch such as `feature/garage-dashboard`.
3. Keep changes focused and explain design decisions.
4. Check the relevant behavior, including mobile layouts and missing-data cases.
5. Open a pull request with a short summary and verification notes.
6. Ryan reviews the change before it is merged into `main`.

AI tools are welcome. Each contributor should understand, explain, and debug the code they submit.

Once tooling is configured, pull requests should run type checking, linting, and a production build. Tests should cover meaningful business rules and user flows.

## Development milestones

| Milestone | Deliverable |
| --- | --- |
| M1 — Foundation | App setup, routing, domain types, mock adapter, and sample truck dashboard |
| M2 — Truck management | Add/edit truck, mileage updates, validation, and empty states |
| M3 — Maintenance | Components, multi-item service records, history, and detail screens |
| M4 — Status and sorting | Maintenance plans, source labels, status calculations, and sorting |
| M5 — Recommendations and polish | Fictional expert notes, component links, mobile usability, and accessibility |
| M6 — Development persistence | Separate development backend/database, API adapter, and verified access controls |

M1–M5 form the proposed mock-data MVP. M6 introduces persistent storage after the core experience is validated.

## Longer-term direction

After the Garage foundation works, possible expansions include:

- **Review My Rig:** A customer requests a paid, structured expert review.
- **Rig Health Report:** An expert records an overall assessment, priorities, suggested tests, and component-specific recommendations.
- **Ask About This Part:** A smaller asynchronous question attached to a component.
- **Consultations:** Connect truck history to scheduled consultations and, eventually, available experts for immediate calls.
- **Reminders and forecasting:** Better planning based on documented schedules, operating conditions, and attributable expert input.
- **Documents and receipts:** Supporting records attached to services and trucks.
- **Parts and shops:** Relevant recommendations, with clear disclosure of any affiliate relationships.
- **Subscriptions and fleet features:** Potential future offerings; pricing and entitlements are undecided.

Experts should receive access to private Garage information through a customer-triggered request they accept or are assigned. They should not be able to browse every owner's Garage. Access must eventually be enforced by the backend.

The scheduled-consultation marketplace remains available as My Rig develops.

## Getting started

Application scaffolding has not been added yet, so there are no working install or run commands at this stage.

The first engineering task is **M1: establish the frontend, shared domain types, mock data interface, and sample truck dashboard**. Add accurate setup instructions when the application exists.

Before implementing a feature, agree on its scope and data contract with Ryan so the dashboard, forms, and maintenance logic fit together.

---

**Product name:** My Rig  
**Development name:** RRC Garage  
**Part of:** Rig Repair Connect / Apex Summit LLC
