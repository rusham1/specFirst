# Data Model: Campus Event & Club Hub

## Event

Represents one campus activity shown in the event listing.

| Field | Type | Required | Rules |
|---|---|---:|---|
| `id` | String | Yes | Unique within the event collection; used to distinguish and render records |
| `title` | String | Yes | Trim surrounding whitespace; must not be empty |
| `category` | String | Yes | Exactly one of `Workshop`, `Social`, or `Sports` |
| `startsAt` | ISO 8601 date-time string | Yes | Must parse as a valid date-time; a newly submitted event must be later than the current time. Persisted events remain valid after they pass, but are no longer upcoming. |
| `location` | String | Yes | Trim surrounding whitespace; must not be empty |
| `description` | String | Yes | Trim surrounding whitespace; must not be empty |

## Relationships and Derived State

- The event collection is an array of `Event` records; each event belongs to exactly one category.
- Upcoming events are records whose `startsAt` is later than the current time.
- The displayed collection is the upcoming set, optionally narrowed to the currently selected category, sorted by `startsAt` ascending.
- The active category filter is view state (`All`, `Workshop`, `Social`, or `Sports`), not part of an event record.

## Persistence

- Store the complete event array as JSON in localStorage under the key `campusEventHub.events`.
- On first visit, initialize from a small array of mock events spanning all three categories and save the initialized collection.
- After successful form validation, add the new event to the collection and persist the updated array before showing success.
- If a storage read or write fails, show a clear error and do not claim that a submission was saved. Do not silently overwrite unreadable saved data.
- localStorage data is local to the browser and origin; clearing that site data removes both mock and submitted event records.

## Validation and State Transitions

1. **Initial load**: Read and validate the saved event array; if the storage key is absent, use and persist the mock array.
2. **Form submission**: Trim text fields, validate required values and category, parse the local date-time, and reject dates not later than the current time.
3. **Persist**: Create a unique `id`, add the valid event, and save the updated full collection. Only after save succeeds, clear the form and report success.
4. **Filter change**: Recompute upcoming events from the current collection, apply the selected category if not `All`, then render in chronological order.
5. **Storage error**: Display an explicit error and prevent a success-shaped submission result; provide guidance to clear invalid site data if stored content cannot be loaded.
