# CaptureOS Layer

## Core baskets

1. Task / Reminder
2. Event / Meeting
3. Idea / Note

## Commands

- `/capture` — enter Capture Mode
- `/normal` — exit Capture Mode

## Defaults

- Task / Reminder: route to a completable task system when available, not an ordinary calendar event.
- Timed Task / Reminder: task due date plus preserved time in title/notes if due-time reminders are not supported.
- Date-only Task / Reminder: task due on that date.
- Undated Task / Reminder: task due tomorrow when clearly actionable, even without an explicit `Task:`/`Reminder:` prefix in Capture Mode.
- Meeting / Call: calendar event, 1 hour.
- Ordinary Event / Appointment: calendar event, 1 hour.
- Large Event: calendar event, 2 hours only when obvious.

## Inbox files

- Task / Reminder: `capture-tasks-reminders.md`
- Event / Meeting: `capture-events-meetings.md`
- Idea / Note: `capture-ideas-notes.md`
