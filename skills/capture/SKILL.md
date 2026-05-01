---
name: capture
description: Enter CaptureOS Capture Mode. Short natural-language messages are treated as captures and routed into three baskets.
version: 0.1.0
author: CaptureOS contributors
license: MIT
metadata:
  hermes:
    tags: [capture, productivity, notes, calendar]
    related_skills: [captureos, normal]
---

# Capture Mode

The user invoked `/capture`, meaning: enter CaptureOS Capture Mode for this session.

## Behavior

Until the user invokes `/normal` or clearly asks to stop capture mode:

1. Treat short natural-language messages as captures by default, not questions.
2. Route every capture into exactly one of three top-level baskets:
   - Task / Reminder
   - Event / Meeting
   - Idea / Note
3. If one message contains multiple items, split into multiple routed actions under those three baskets.
4. Do not expose extra top-level categories to the user.
5. Ask only when ambiguity materially changes the action.

## Defaults

- Task / Reminder: create in the configured task system when available, so the item can be marked complete.
- Timed Task / Reminder: keep as a task with the due date; preserve the mentioned time in the task title/notes if the provider does not support due-time reminders.
- Date-only Task / Reminder: task due on that date.
- Recurring completable Task / Reminder: use native task recurrence when the provider/API supports it. If the provider UI supports recurrence but the API does not, avoid bulk-creating long horizons by default; create a small idempotent scheduled check that runs on each occurrence date, verifies the next occurrence exists, creates it only if missing, and reports created vs skipped.
- Undated Task / Reminder: task due tomorrow when the item is clearly actionable, even if the user did not write `Task:` or `Reminder:` explicitly.
- Only create a calendar event for a task/reminder when the user explicitly asks for a time-block or the wording is clearly a meeting/call/event.
- Meeting / Call: calendar event, 1 hour.
- Ordinary Event / Appointment: calendar event, 1 hour.
- Large Event: calendar event, 2 hours only when context clearly implies it

## Response style

Be concise. Confirm what was captured and where it went.
