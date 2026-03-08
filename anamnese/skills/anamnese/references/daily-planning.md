# Daily Planning Reference

Step-by-step workflow for combining Anamnese tasks with calendar events into a unified daily plan.

## Planning Steps

### 1. Load Context
Call `get_user_profile` to get the full picture: overdue tasks, today's tasks, tomorrow's tasks, facts, goals, and recent moments.

### 2. Get Calendar Events
Check if a calendar MCP is connected (Google Calendar, Microsoft 365, or similar):
- **If connected:** Fetch today's events to build a complete timeline
- **If not connected:** Plan based on tasks only, and suggest connecting a calendar MCP via `/mcp`

### 3. Identify Free Time
When calendar events are available, analyze gaps in the schedule:
- Account for 5-10 minutes of transition time between meetings
- Note which gaps are large enough for deep work vs. only suitable for quick tasks

### 4. Check Backlog
Call `search_tasks` with `unscheduled: true` to find unscheduled tasks. Suggest which backlog tasks could fill free time, prioritizing by:
1. High-priority tasks first
2. Tasks with approaching deadlines
3. Tasks that align with active goals
4. Quick wins that fit small time gaps

### 5. Handle Overdue Tasks
For any overdue tasks, ask the user whether to:
- Reschedule to today (`update_task` with new `scheduled_date`)
- Reschedule to a future date
- Mark as completed
- Skip (for recurring tasks, `update_task` with `is_skipped: true`)

### 6. Ask About New Tasks
Ask: "Is there anything outside your recurring tasks that needs to get done today?" Create new tasks with `create_task` as needed.

### 7. Consider Tomorrow
If today has significant free time, look at tomorrow's tasks from the profile data. Suggest pulling forward tasks that would be better done today -- but don't overload the day.

### 8. Present Final Plan
Present the plan in a clear time-block or table format. Ask if the user wants any changes. Use `update_task` for adjustments.

## Timezone Handling

- Detect the user's timezone from their profile facts
- If timezone is unknown, ask before presenting the schedule
- Present all times in the user's local timezone
- Explicitly state which timezone is being used

## Low-Data Onboarding

If the user's profile has fewer than ~5 facts, take the opportunity to ask about:
- Typical weekday routine (wake time, work hours, lunch, exercise)
- Typical weekend routine
- Regular commitments not in calendar or tasks
- Preferred working patterns (e.g., deep work in mornings)

Save responses using `save_memory` (type: "fact") to personalize future planning sessions.
