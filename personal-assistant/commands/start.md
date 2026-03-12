---
description: Onboard and authenticate with Anamnese, check connected MCPs, and bootstrap your personal profile
---

Follow these steps to get the user set up with Anamnese as their personal life assistant:

## Step 1: Authenticate

Call `get_user_profile` to check if Anamnese is authenticated.

- **If it returns a 401 or auth error:** Tell the user to run `/mcp` to authenticate via browser, then try again.
- **If it succeeds:** Continue to Step 2.

## Step 2: Check Integrations

Check which integrations are connected by attempting to use them:
- **Calendar:** Try calling a Google Calendar tool. Note whether calendar is available.
- **Gmail:** Try calling a Gmail tool. Note whether Gmail is available.

Report which integrations are connected and which aren't.

## Step 3: Assess Profile Richness

Look at the profile data returned from `get_user_profile`:
- Count the number of facts stored
- Check if goals exist
- Check if tasks exist

**If the profile has >= 5 facts:** Skip to Step 5 (Orientation).

**If the profile is sparse (< 5 facts):** Continue to Step 4.

## Step 4: Get to Know You

Run a friendly "get to know you" conversation focused on personal life. Ask about:

1. **Name and life situation** -- "What's your name? Tell me a bit about yourself."
2. **Goals and aspirations** -- "What are your main goals right now -- personal, health, financial, or otherwise?"
3. **Daily routines** -- "What does a typical day look like for you?"
4. **Wellness** -- "Any health or wellness habits you're tracking or want to build?"
5. **Financial** -- "Any financial goals you're working toward?"

Save all answers using the appropriate tools:
- Personal details -> `save_memory` (type: "fact")
- Goals -> `save_goal`
- Routines/patterns -> `save_memory` (type: "fact")
- Health info -> `save_memory` (type: "fact")

Don't ask all questions at once. Have a natural conversation, ask 2-3 questions at a time, and save as you go.

## Step 5: Orientation

Show the user what's available:

**MCP prompts (type `/` to see all):**
- `/save-memory` -- Save conversation insights to memory
- `/memory-cleanup` -- Audit and deduplicate your memory
- `/add-task` -- Create a new task
- `/plan-my-day` -- Guided daily planning session
- `/learn-more` -- Ask Anamnese to learn more about you

**Skills (activate automatically as you chat):**
- **Anamnese** -- Core memory, tasks, goals, notes, and proactive capture
- **Goal Planning** -- Tracks personal goals, life milestones, and aspirations
- **Financial Awareness** -- Captures budget decisions, financial goals, and spending patterns
- **Wellness** -- Tracks health habits, exercise, sleep, nutrition, and medical info

**Tips:**
- Anamnese remembers across all your AI apps (Claude, ChatGPT, Claude Code, Cursor) and devices
- Just chat naturally -- proactive capture saves important details automatically
- Use `/plan-my-day` each morning to organize your day
