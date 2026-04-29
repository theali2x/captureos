---
name: captureos
description: Three-basket universal capture router for Hermes Agent: Task / Reminder, Event / Meeting, Idea / Note.
version: 0.2.0
author: CaptureOS contributors
license: MIT
metadata:
  hermes:
    tags: [capture, notes, calendar, productivity, markdown]
    related_skills: [capture, normal]
---

# CaptureOS

CaptureOS is a universal capture layer for Hermes Agent and compatible assistant workflows.

## Core principle

Capture anything once. The assistant decides which of three baskets it belongs in and updates the right destination.

Prefer clean living updates over raw dumps.

## Core baskets

Classify every capture into exactly one of three top-level user-facing baskets:

1. Task / Reminder
   - todos, follow-ups, promises, deadlines, recurring reminders, scheduled task blocks

2. Event / Meeting
   - calls, meetings, calendar events, trips, appointments, event notes, meeting notes

3. Idea / Note
   - ideas, project notes, people updates, opportunities, journal/reflections, links, durable wiki knowledge, reusable build ideas, dated outputs/runbooks

Subtypes may exist internally for routing, but do not expose more than these three baskets in the core capture layer.

## Mode commands

- `/capture` = enter Capture Mode for the current session
- `/normal` = exit Capture Mode and return to normal assistant behavior

Explicit prefixes still work in normal mode: `Task:`, `Reminder:`, `Meeting:`, `Event:`, `Idea:`, `Capture:`, and `Process this:`.

## Default destinations

Task / Reminder:
- Clear dated or timed items go to the configured task system when available, so they can be marked complete.
- Do not create tasks/reminders as ordinary calendar events unless the user explicitly asks for a time-block or the wording is clearly a meeting/call/event.
- Open/undated items that should not be tasked/calendar-routed go to the configured Task / Reminder inbox.

Event / Meeting:
- Clear scheduled blocks go to the configured calendar when available.
- Meeting/event notes go to the Event / Meeting inbox when no stronger destination exists.

Idea / Note:
- Prefer the strongest existing knowledge-base page when obvious.
- If no better destination is obvious, save to the Idea / Note inbox.
- Raw evidence should be stored separately only when explicitly requested or when provenance matters.

## Calendar defaults

- Meeting / Call: 1 hour
- Ordinary Event / Appointment: 1 hour
- Large Event: 2 hours only when context clearly implies a longer block, such as dinner, conference, party, workshop, or multi-hour activity
- Timed Task / Reminder: task due date plus preserved time in title/notes if the task provider does not support due-time reminders
- Date-only Task / Reminder: task due on that date
- Undated Task / Reminder: task due tomorrow when the item is clearly actionable, even if the user did not write `Task:` or `Reminder:` explicitly in Capture Mode
- Default calendar reminders: 24 hours and 1 hour before, for events/meetings when the calendar provider supports it

## Ask-first policy

Ask before:

- deleting calendar events or notes
- moving/rescheduling existing events unless explicitly requested
- creating calendar items when there is a conflict or meaningful ambiguity
- sending emails/messages
- saving sensitive/private personal details
- modifying immutable/raw source files

Act directly when:

- the capture is low-risk and destination is obvious
- a calendar item is clear and non-conflicting
- updating a Markdown inbox is straightforward

## Process this

For messy notes or transcripts:

1. Extract tasks/reminders, events/meetings, and ideas/notes.
2. Group proposed actions by the three baskets.
3. If many files/events would be changed, preview before applying.
4. Apply approved updates and summarize changed files/events.

## Daily debrief

Ask concise prompts:

- What happened today?
- Who did you speak to?
- Any promises or follow-ups?
- Any meetings/events/reminders to calendar?
- Any ideas worth keeping?
- Anything for work, clients, projects, or reusable processes?
- Anything personally important?

Then route updates into the three baskets.
