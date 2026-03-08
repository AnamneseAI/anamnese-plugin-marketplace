---
name: daily-planning
description: "This skill should be used when the user discusses planning their work day, time-blocking, scheduling deep work, managing meetings, or organizing their work schedule. Triggers on phrases like \"plan my day\", \"what's on my calendar\", \"when should I work on\", \"block time for\", or any work scheduling discussion."
user-invocable: false
---

# Daily Planning

Help the user plan and optimize their work day through scheduling, time-blocking, and calendar integration.

## When to Activate

- User asks about planning their day or week
- User mentions scheduling or time-blocking
- User asks what's on their calendar
- User discusses fitting tasks into their schedule
- User mentions deep work, focus time, or meeting management

## Planning Workflow

When the user wants to plan their day:

1. Gather context: existing tasks, goals, calendar events, and deadlines
2. Identify free time blocks between meetings and commitments
3. Apply the Eisenhower matrix to prioritize what to work on
4. Suggest task placement based on priority, deadlines, and energy levels
5. Present a clear time-blocked plan

## Prioritization with the Eisenhower Matrix

Help the user sort tasks into four quadrants:
- **Urgent + Important** -- do these first (deadlines, critical issues)
- **Important + Not Urgent** -- schedule these into focus blocks (strategic work, skill building)
- **Urgent + Not Important** -- batch or delegate (most emails, routine requests)
- **Neither** -- drop or defer (busywork, low-value distractions)

## Realistic Capacity Planning

- Most people can sustain 4-6 hours of focused work per day -- plan accordingly
- Account for meeting recovery time (meetings drain energy beyond their duration)
- Leave 20-30% of the day unscheduled for unexpected work and overflow
- Identify the user's "must-win" for the day -- the one thing that would make the day a success

## Time-Blocking Principles

- **Deep work first** -- schedule high-concentration tasks during the user's best focus hours
- **Buffer time** -- leave 5-10 minutes between meetings for transitions
- **Energy matching** -- creative work in high-energy slots, admin in low-energy slots
- **Batch similar tasks** -- group emails, messages, and quick tasks together
- **Protect focus blocks** -- suggest at least one 90-minute uninterrupted block

## Calendar Integration

When calendar events are available:
- Build a complete timeline combining events and tasks
- Identify realistic free time (accounting for transitions)
- Flag schedule conflicts or overcommitment
- Suggest which tasks fit which gaps

When no calendar is connected:
- Plan based on tasks and the user's stated work hours
- Suggest connecting Google Calendar or Microsoft 365 via `/mcp`

## Weekly Planning

When the user discusses the week ahead:
- Review upcoming deadlines and priorities
- Identify days with heavy meetings vs. open days
- Suggest spreading tasks across the week by priority
- Flag potential conflicts or overloaded days
