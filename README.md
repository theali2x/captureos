# CaptureOS

CaptureOS is a lightweight, private-first capture router for Hermes Agent.

It turns messy natural-language input — quick texts, voice notes, meeting notes, pasted ideas, reminders — into exactly one of three simple baskets:

1. Task / Reminder
2. Event / Meeting
3. Idea / Note

The point is not to create another dumping ground. CaptureOS gives an AI assistant a clean operating model for deciding what something is, where it belongs, and when it should ask before acting.

## Why CaptureOS?

Most capture systems either over-classify everything or let notes pile up forever. CaptureOS keeps the user-facing model intentionally small:

- Tasks and reminders are things to do or remember.
- Events and meetings are things that occupy time on a calendar.
- Ideas and notes are durable knowledge, context, links, reflections, or project material.

Everything else is an internal subtype, not another basket the user has to manage.

## What it includes

- Hermes Agent skills for `/capture`, `/normal`, and the core `captureos` routing rules
- Markdown inbox templates for the three baskets
- A custom commands template
- A polished step-by-step setup guide
- Clear examples for common captures
- Validation and lightweight secret-scan scripts
- Optional patch file for native Hermes slash-command registration

## Core commands

```text
/capture
```

Enter Capture Mode. Short natural-language messages are treated as captures by default.

```text
/normal
```

Exit Capture Mode and return to normal assistant behavior.

Explicit prefixes such as `Task:`, `Reminder:`, `Meeting:`, `Event:`, `Idea:`, `Capture:`, and `Process this:` can still be used outside Capture Mode.

## How it works

### Example 1: task / reminder

Input:

```text
Follow up with Sarah Friday 11am about the proposal
```

CaptureOS classifies it as:

```text
Basket: Task / Reminder
Default duration: 1 hour if placed on a calendar
Action: create a reminder/task block if calendar integration is configured, otherwise save to the Task / Reminder inbox
```

### Example 2: event / meeting

Input:

```text
Dentist tomorrow 3pm
```

CaptureOS classifies it as:

```text
Basket: Event / Meeting
Default duration: 1 hour
Action: create a calendar event if the time is clear and there is no conflict
```

### Example 3: idea / note

Input:

```text
Idea: build a reusable onboarding agent that turns client calls into implementation plans
```

CaptureOS classifies it as:

```text
Basket: Idea / Note
Action: save to the strongest matching knowledge-base page, or the Idea / Note inbox if no better destination exists
```

### Example 4: messy debrief

Input:

```text
Process this: met Jordan today. He wants the new landing page by Thursday. Also had an idea for a simple weekly client report generator.
```

CaptureOS extracts:

```text
Task / Reminder: deliver or follow up on the landing page by Thursday
Event / Meeting: met Jordan today
Idea / Note: weekly client report generator idea
```

## Default timing rules

- Timed Task / Reminder: 1 hour
- Date-only Task / Reminder: all-day
- Undated Task / Reminder: tomorrow all-day
- Meeting / Call: 1 hour
- Ordinary Event / Appointment: 1 hour
- Large Event: 2 hours only when context clearly implies a longer block
- Calendar reminders: 24 hours and 1 hour before, when supported by the calendar provider

## Ask-first policy

CaptureOS is designed to act when the action is obvious and low risk, and ask when it matters.

Act directly when:

- the capture has a clear destination
- a calendar item is clear and non-conflicting
- saving to a local Markdown inbox is straightforward

Ask first before:

- deleting anything
- rescheduling existing events
- creating events when there is a conflict or meaningful ambiguity
- sending messages or emails
- storing sensitive personal details
- modifying raw/immutable evidence files

## Quick setup

```bash
git clone https://github.com/OWNER/captureos.git
cd captureos
./scripts/install.sh --vault ~/Documents/CaptureVault
```

Then restart Hermes or its messaging gateway if needed, and try:

```text
/capture
Dentist tomorrow 3pm
Idea: a tiny habit tracker that uses voice notes
/normal
```

For the full setup flow, see `QUICKSTART.md`. For calendar, email, and messaging access, see `SETUP_INTEGRATIONS.md`.

## Repository structure

```text
CaptureOS/
├── skills/                  # Hermes skills
│   ├── capture/
│   ├── normal/
│   └── captureos/
├── templates/               # Markdown inbox and command templates
├── config/                  # Example configuration
├── examples/                # Example capture flows
├── SETUP_INTEGRATIONS.md    # Calendar, email, and messaging setup
├── scripts/                 # install, validate, and secret scan scripts
└── docs/                    # optional integration notes
```

## Security

This repository should contain only reusable system instructions, templates, examples, and scripts. Do not commit real tokens, OAuth files, account identifiers, calendar IDs, private vault data, client data, or personal contact data.

Before publishing or accepting contributions, run:

```bash
./scripts/validate.sh
./scripts/secret-scan.sh
```

For public release, also run a dedicated scanner such as gitleaks or trufflehog. See `SECURITY.md`.

## Status

Public-ready alpha. The core model is intentionally small and stable; integrations can be added around it.

## License

MIT. See `LICENSE`.
