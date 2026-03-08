---
name: anamnese
description: "Load this skill at the start of every conversation. Anamnese is the user's persistent memory and productivity system -- it should always be active. Call get_user_profile first to load context, then continuously capture meaningful information: personal details, preferences, decisions, tasks, goals, schedules, and knowledge worth saving. You can also use notes as your own persistent memory across sessions -- prefix descriptions with \"ai-memory:\" when using save_note to store operational notes: interaction patterns, self-corrections, behavioral preferences, or anything you want to remember about how to assist this user."
user-invocable: false
---

# Anamnese

Anamnese is the user's cloud-persistent memory and productivity system. Use it to store, retrieve, and manage personal information, tasks, goals, and notes across sessions.

## Start Every Conversation

Call `get_user_profile` at the beginning of each conversation to load the user's full context: facts, goals, tasks, moments, and profile data.

## Proactive Capture

Be the user's memory. Capture what matters automatically -- don't wait to be asked.

As you converse, continuously identify information worth remembering and save it immediately using the appropriate tool. Don't ask "should I save this?" -- just save it if it's meaningful.

### What to Capture

| Signal | Action |
|--------|--------|
| Personal details ("I moved to Austin", "I prefer TypeScript") | `save_memory` type="fact" |
| Decisions and outcomes ("We chose Postgres", "I got the offer") | `save_memory` type="moment" with `occurred_at` |
| Process explanations, corrections, technical context | `save_note` |
| Commitments ("I need to finish by Friday", "Remind me to...") | `create_task` |
| Aspirations ("I want to learn Rust", "Goal is to ship v2") | `save_goal` |
| Your own observation, self-correction, or interaction insight | `save_note` with `"ai-memory:"` description prefix |

### Capture Rules

1. **Check before saving** -- search first to avoid duplicates
2. **Be selective** -- save what's useful for future conversations, not passing remarks
3. **Use the right type** -- facts for stable truths, moments for events, notes for knowledge, tasks for action items, goals for aspirations
4. **Capture corrections** -- when the user corrects you, update the relevant fact or note immediately
5. **Don't interrupt** -- save in the background without disrupting the conversation flow

## Data Types Overview

### Facts (type="fact")
Stable truths that persist for months or years: identity, preferences, relationships, health, skills, habits. Save with `save_memory` type="fact".

### Moments (type="moment")
Time-bound events at a specific point. Always include `occurred_at`. Save with `save_memory` type="moment".

### Notes
Learned knowledge, procedures, guidelines, and technical context. Use `save_note` for processes, how-tos, architecture details, and user corrections.

#### AI Memory
You can use notes as your own persistent memory across sessions. Prefix the description with `"ai-memory:"` to distinguish your operational notes from user-created ones. Use this for interaction patterns you've noticed, self-corrections, behavioral preferences the user expressed, or approaches you've learned work well -- anything you as an AI want to remember about how to assist this user. Use `search_notes` with the `"ai-memory"` keyword to find your own notes from previous sessions.

### Tasks
One-off and recurring tasks with priorities, deadlines, and scheduling. Use `create_task`. Provide `freq` for recurring tasks (daily, weekly, monthly). See `references/task-management.md` for recurring task patterns and advanced usage.

### Goals
Long-term objectives and aspirations. Use `save_goal`.

## Core Tools

### Memory
`save_memory`, `search_memories`, `update_memory`, `delete_memory`, `get_user_profile`

### Notes
`save_note`, `search_notes`, `get_note`, `update_note`, `delete_note`

### Tasks
`create_task`, `search_tasks`, `update_task`, `delete_task`

### Goals
`save_goal`, `search_goals`, `update_goal`, `delete_goal`

## Best Practices

1. **Check before saving** -- use `search_memories` or `search_notes` to avoid duplicates
2. **Update over create** -- if a memory or note already exists on the topic, use `update_memory` or `update_note`
3. **Tag appropriately** -- use free-form tags (any string, max 5 per item, max 50 chars each)
4. **Prefer moments for events** -- when in doubt between fact and moment, choose moment (timestamped)
5. **Ask about priority** for tasks if not obvious from context
6. **Confirm deadlines** -- make sure you understood the date correctly

## Reference Files

For detailed workflows, load these reference files when the relevant domain is active:

- `references/memory-management.md` -- Detailed guidance on facts, moments, and notes
- `references/task-management.md` -- Recurring tasks, scheduling patterns, and task lifecycle
- `references/daily-planning.md` -- Step-by-step daily planning workflow with calendar integration
