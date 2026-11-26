# User Interface Contract

## Event listing

- Show a page heading identifying the Campus Event & Club Hub.
- Display each upcoming event as a card with its title, category, local date and time, location, and description.
- Present category controls for All, Workshop, Social, and Sports.
- Selecting a category updates the visible cards without removing events from the stored collection.
- Sort visible cards from soonest to latest.
- When no events match, show a clear empty-state message.

## Event submission

- Provide labeled controls for title, category, date and time, location, and description.
- Require every field and reject whitespace-only text values.
- Reject dates and times that are not in the future.
- On validation failure, identify the invalid or missing field and preserve other entered values.
- On successful storage, confirm submission and make the event available in All and its matching category.
- If storage fails, show an error and do not report success.

## Accessibility and responsive behavior

- Use native form controls, associated visible labels, and buttons operable by keyboard.
- Make validation and storage feedback available as readable text, not color alone.
- Keep the controls and event cards usable on narrow and wide viewports using responsive CSS layout.
