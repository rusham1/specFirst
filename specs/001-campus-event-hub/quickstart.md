# Quickstart: Campus Event & Club Hub

## Prerequisites

- A current desktop or mobile browser with JavaScript and localStorage enabled.
- Python 3 for serving the static files locally; no package installation or build step is required.

## Run locally

From the project root, start a static file server:

```sh
python3 -m http.server 8000
```

Open `http://localhost:8000` in a browser. Stop the server with `Ctrl+C`.

## Validation scenarios

1. **Initial event list**: On a fresh browser origin, confirm example events appear as cards, include all three categories, and are ordered from soonest to latest.
2. **Category filtering**: Select Workshop, Social, and Sports in turn. Confirm each view contains only events in the selected category. Select All and confirm all upcoming events return.
3. **Successful submission**: Submit an event with a non-empty title, supported category, future date and time, location, and description. Confirm success feedback and that the event appears in the list and the matching category.
4. **Persistence**: Reload the page in the same browser and confirm the submitted event remains available.
5. **Invalid input**: Try submitting whitespace-only required fields and a past date and time. Confirm each is rejected with a clear message and is not added to the list.
6. **Empty state**: Temporarily remove all entries from the mock event array in `app.js`, clear site data for `localhost:8000`, and reload. Confirm the page explains that no upcoming events are available. To check a category-specific empty state, leave out mock events for one category and select that category.

Restore the mock event array and clear site data for `localhost:8000` after this check.
