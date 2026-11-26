# Tasks: Campus Event & Club Hub

**Input**: Design documents from `specs/001-campus-event-hub/`

**Prerequisites**: `plan.md`, `spec.md`, `research.md`, `data-model.md`, `contracts/ui.md`, and `quickstart.md`

**Tests**: No automated test tasks are included because the feature specification does not request a test-first workflow. Validate each increment using the independent browser checks below and the final `quickstart.md` scenarios.

**Organization**: Tasks are grouped by user story so each increment can be implemented and checked independently after its listed prerequisites.

## Format: `[ID] [P?] [Story] Description`

- **[P]**: Can run in parallel because it works in a different file and has no dependency on another incomplete task.
- **[Story]**: User-story traceability label; setup, foundational, and polish tasks have no story label.
- Every task names the application or design file it changes.

## Phase 1: Setup

**Purpose**: Establish the three-file static application shell.

- [X] T001 [P] Create the semantic page shell, shared status region, event-list container, and stylesheet/script references in `index.html`.
- [ ] T002 [P] Add base typography, color tokens, focus visibility, and responsive page layout in `styles.css`.

## Phase 2: Foundational

**Purpose**: Establish the shared event collection and storage behavior required by all user stories.

- [ ] T003 Initialize mock events with dates generated relative to the current time and localStorage load/save state in `app.js`; follow `data-model.md` for `Event.id` uniqueness, `Event.title` trimming and non-empty values, `Event.category` allowed values, `Event.startsAt` date-time parsing, and non-empty trimmed `Event.location` and `Event.description`. Enforce future dates for new submissions, but allow persisted events to become past events. Surface invalid or unavailable storage through the status region in `index.html` without silently replacing saved data.

**Checkpoint**: Shared event state is available; story implementation can begin.

## Phase 3: User Story 1 - Browse Upcoming Events (Priority: P1) 🎯 MVP

**Goal**: Show students useful, chronological event cards immediately, including a clear empty state when no events are upcoming.

**Independent Test**: Load the page with mock upcoming events and confirm each card shows its key details in chronological order. Confirm an empty state appears when there are no upcoming events.

### Implementation for User Story 1

- [ ] T004 [P] [US1] Render upcoming events from the shared collection as chronological cards with title, category, local date and time, location, and description; show the empty state when none qualify in `app.js`.
- [ ] T005 [P] [US1] Style the event list and cards for narrow and wide viewports in `styles.css`.

**Checkpoint**: User Story 1 is browseable and independently verifiable.

## Phase 4: User Story 2 - Filter Events by Category (Priority: P2)

**Goal**: Let students filter the upcoming cards by Workshop, Social, Sports, or All.

**Independent Test**: With User Story 1 available, select each category and verify only matching upcoming cards remain. Select All and verify the full upcoming list returns; verify an empty state for a category with no matching events.

### Implementation for User Story 2

- [ ] T006 [P] [US2] Add All, Workshop, Social, and Sports filter buttons using `.category-filter`, `data-category`, and `.is-active` for the selected option in `index.html`.
- [ ] T007 [US2] Connect `.category-filter` buttons and their `data-category` values to the shared event collection; update `.is-active` and rerender matching upcoming cards, preserving the All view and category-specific empty state, in `app.js`.
- [ ] T008 [P] [US2] Style `.category-filter` controls, the `.is-active` state, and keyboard focus in `styles.css`.

**Checkpoint**: User Story 2 works without changing or removing stored events.

## Phase 5: User Story 3 - Submit a New Event (Priority: P3)

**Goal**: Allow students to submit valid future events and retain successful submissions across reloads.

**Independent Test**: With User Stories 1 and 2 available, submit a valid event, confirm it appears in All and its category, then reload and verify it remains. Confirm blank, whitespace-only, and past-date submissions are rejected with feedback.

### Implementation for User Story 3

- [ ] T009 [P] [US3] Add labeled title, category, local date/time, location, and description controls plus validation and submission feedback regions in `index.html`.
- [ ] T010 [P] [US3] Style the event form, field errors, and success/storage feedback in `styles.css`.
- [ ] T011 [US3] Validate and submit events in `app.js`; follow `data-model.md` for `Event.id` uniqueness, `Event.title` trimming and non-empty values, `Event.category` allowed values, future `Event.startsAt` interpreted in local time, and non-empty trimmed `Event.location` and `Event.description`. Persist before showing success, preserve entered values after validation or storage errors, and make the saved event discoverable in All and its matching category.

**Checkpoint**: Valid student submissions are visible and survive a reload in the same browser.

## Phase 6: Polish & Cross-Cutting Validation

**Purpose**: Validate the complete MVP against its user-facing contract.

- [ ] T012 Run every scenario in `specs/001-campus-event-hub/quickstart.md` in a browser; check keyboard operation, feedback readability, and narrow/wide layouts, correcting issues in `index.html`, `styles.css`, and `app.js`.

## Dependencies & Execution Order

### Phase Dependencies

- **Setup (Phase 1)**: T001 and T002 have no dependencies and can run in parallel.
- **Foundational (Phase 2)**: T003 depends on T001's page/status structure and blocks all user stories.
- **User Story 1 (Phase 3)**: Depends on the shared event collection from T003.
- **User Story 2 (Phase 4)**: Depends on User Story 1's card renderer so category changes can update the existing listing.
- **User Story 3 (Phase 5)**: Depends on User Stories 1 and 2 so submitted events update the listing and remain discoverable with the active category filter.
- **Polish (Phase 6)**: Depends on the user stories selected for delivery; for the full MVP, complete all three first.

### User Story Dependencies

- **US1 (P1)**: Depends on Setup and Foundational; no dependency on another user story.
- **US2 (P2)**: Depends on US1's event list and renderer.
- **US3 (P3)**: Depends on US1's event list and US2's category-filter state.

### Parallel Opportunities

- T001 and T002 can run in parallel.
- After T003, T004 and T005 can run in parallel.
- During US2, T006 and T008 can run in parallel; T007 uses the agreed filter button data attributes and active-state class.
- During US3, T009 and T010 can run in parallel; T011 follows both.

## Parallel Example: User Story 1

```text
After T003 is complete:
- T004: Render upcoming event cards and empty state in app.js
- T005: Style event cards and list layout in styles.css
```

## Implementation Strategy

### MVP First (User Story 1)

1. Complete Setup and Foundational tasks.
2. Complete US1 to render example upcoming event cards.
3. Validate US1 independently using its browser check.
4. Deliver US1 as the first useful increment.

### Incremental Delivery

1. Add US2 category filters after US1; validate all four filter choices and the empty state.
2. Add US3 submission and persistence after US2; validate form errors, successful save, filtering, and reload persistence.
3. Complete the cross-cutting browser checks in T012.

## Notes

- All application behavior is implemented in the three planned files: `index.html`, `styles.css`, and `app.js`.
- [P] marks tasks in separate files that can proceed without waiting on each other.
- Story labels map to the priorities and acceptance scenarios in `spec.md`.
- Field constraints are defined in `data-model.md`; T003 and T011 explicitly cite each constrained `Event` field.
