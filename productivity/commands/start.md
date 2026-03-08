---
description: Onboard and authenticate with Anamnese, check connected MCPs, and bootstrap your work profile
---

Follow these steps to get the user set up with Anamnese as their productivity system:

## Step 1: Authenticate

Call `get_user_profile` to check if Anamnese is authenticated.

- **If it returns a 401 or auth error:** Tell the user to run `/mcp` to authenticate via browser, then try again.
- **If it succeeds:** Continue to Step 2.

## Step 2: Check Companion MCPs

Check which companion MCPs are connected by attempting to use them:
- **Calendar:** Try calling a Google Calendar or Microsoft 365 calendar tool. Note whether calendar is available.
- **Slack:** Try listing Slack channels or similar. Note whether Slack is available.
- **Project tracking:** Check for Notion, Linear, Atlassian if relevant.

Report which MCPs are connected and which aren't.

## Step 3: Assess Profile Richness

Look at the profile data returned from `get_user_profile`:
- Count the number of facts stored
- Check if goals exist
- Check if tasks exist

**If the profile has >= 5 facts:** Skip to Step 5 (Orientation).

**If the profile is sparse (< 5 facts):** Continue to Step 4.

## Step 4: Get to Know You

Run a friendly "get to know you" conversation focused on work and productivity. Ask about:

1. **Name and role** -- "What's your name and what do you do?"
2. **Current projects** -- "What are you currently working on?"
3. **Work patterns** -- "What does a typical work day look like for you?"
4. **Career goals** -- "What are your main professional goals right now?"
5. **Tools and processes** -- "What tools and workflows are central to your work?"

Save all answers using the appropriate tools:
- Personal/work details -> `save_memory` (type: "fact")
- Goals -> `save_goal`
- Routines/patterns -> `save_memory` (type: "fact")
- Process knowledge -> `save_note`

Don't ask all questions at once. Have a natural conversation, ask 2-3 questions at a time, and save as you go.

## Step 5: Suggest Companion MCPs

For any companion MCPs that aren't connected, suggest relevant ones:

- **No calendar connected:** "For daily planning with calendar integration, connect Google Calendar or Microsoft 365. They're already configured in this plugin -- just run `/mcp` to authenticate."
- **No Slack connected:** "For communication context, connect Slack -- also pre-configured."
- **No Notion connected:** "For docs and wiki access, connect Notion."
- **No project tracker:** "For project tracking, connect Linear, Atlassian (Jira), Asana, Monday, or ClickUp."

Only suggest MCPs that are relevant to the user's role and context.

## Step 6: Orientation

Show the user what's available:

**MCP prompts (type `/` to see all):**
- `/save-memory` -- Save conversation insights to memory
- `/memory-cleanup` -- Audit and deduplicate your memory
- `/add-task` -- Create a new task
- `/plan-my-day` -- Guided daily planning session
- `/learn-more` -- Ask Anamnese to learn more about you

**Skills (activate automatically as you chat):**
- **Anamnese** -- Core memory, tasks, goals, notes, and proactive capture
- **Daily Planning** -- Work day scheduling, time-blocking, deep work patterns
- **Career Growth** -- Professional development, skill building, performance tracking
- **Knowledge Management** -- Capturing learnings, documenting processes

**Tips:**
- Anamnese remembers across all your AI clients and devices
- Just chat naturally -- proactive capture saves important details automatically
- Use `/plan-my-day` each morning to organize your work day
