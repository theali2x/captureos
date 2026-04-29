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

- Timed Task / Reminder: 1 hour
- Date-only Task / Reminder: all-day
- Undated Task / Reminder: tomorrow all-day when the item is clearly actionable, even if the user did not write `Task:` or `Reminder:` explicitly
- Meeting / Call: 1 hour
- Ordinary Event / Appointment: 1 hour
- Large Event: 2 hours only when context clearly implies it

## Response style

Be concise. Confirm what was captured and where it went.
