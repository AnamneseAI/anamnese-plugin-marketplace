---
description: Onboard and authenticate with Anamnese Assistant, check connected integrations, and set up your personal and work profile
---

Follow these steps to get the user set up with the Anamnese Assistant:

## Step 1: Authenticate

Call `get_user_profile` to check if Anamnese is authenticated.

- **If it returns a 401 or auth error:** Tell the user to run `/mcp` to authenticate via browser, then try again.
- **If it succeeds:** Continue to Step 2.

## Step 2: Check Integrations

Check which integrations are connected by attempting to use them:
- **Calendar:** Try calling a Google Calendar or Microsoft 365 calendar tool. Note whether calendar is available.
- **Gmail:** Try calling a Gmail tool. Note whether Gmail is available.
- **Slack:** Try listing Slack channels or similar. Note whether Slack is available.
- **Project tracking:** Check for Notion, Linear, Atlassian if relevant.

Report which integrations are connected and which aren't.

## Step 3: Assess Profile Richness

Look at the profile data returned from `get_user_profile`:
- Count the number of facts stored
- Check if goals exist
- Check if tasks exist

**If the profile has >= 5 facts:** Skip to Step 5 (Suggest Integrations).

**If the profile is sparse (< 5 facts):** Continue to Step 4.

## Step 4: Get to Know You

Run a friendly "get to know you" conversation covering both personal and professional life. Ask about:

1. **Name and life situation** -- "What's your name? Tell me a bit about yourself."
2. **Work and role** -- "What do you do? What are you currently working on?"
3. **Goals** -- "What are your main goals right now -- personal, professional, health, financial, or otherwise?"
4. **Daily routines** -- "What does a typical day look like for you?"
5. **Wellness** -- "Any health or wellness habits you're tracking or want to build?"
6. **Tools** -- "What tools and workflows are central to your work?"

Save all answers using the appropriate tools:
- Personal/work details -> `save_memory` (type: "fact")
- Goals -> `save_goal`
- Routines/patterns -> `save_memory` (type: "fact")
- Process knowledge -> `save_note`

Don't ask all questions at once. Have a natural conversation, ask 2-3 questions at a time, and save as you go.

## Step 5: Suggest Integrations

For any integrations that aren't connected, suggest relevant ones:

- **No calendar connected:** "For daily planning with calendar integration, connect Google Calendar or Microsoft 365. They're already configured in this plugin -- just run `/mcp` to authenticate."
- **No Slack connected:** "For communication context, connect Slack -- also pre-configured."
- **No Notion connected:** "For docs and wiki access, connect Notion."
- **No project tracker:** "For project tracking, connect Linear, Atlassian (Jira), Asana, Monday, or ClickUp."

Only suggest integrations that are relevant to the user's role and context.

## Step 6: Orientation

Show the user what's available:

**MCP prompts (type `/` to see all):**
- `/save-memory` -- Save conversation insights to memory
- `/memory-cleanup` -- Audit and deduplicate your memory
- `/add-task` -- Create a new task
- `/plan-my-day` -- Guided daily planning session
- `/learn-more` -- Ask Anamnese to learn more about you

**Skills (activate automatically as you chat):**
- **Goal Planning** -- Tracks personal goals, life milestones, and aspirations using the SMART framework
- **Financial Awareness** -- Captures budget decisions, financial goals, and spending patterns
- **Wellness** -- Tracks health habits, exercise, sleep, nutrition, and medical info
- **Daily Planning** -- Work day scheduling, time-blocking, and Eisenhower prioritization
- **Career Growth** -- Professional development, skill building, performance tracking
- **Knowledge Management** -- Capturing learnings, documenting processes, building a personal knowledge base

**Tips:**
- Anamnese remembers across all your AI apps (Claude, ChatGPT, Claude Code, Cursor) and devices
- Just chat naturally -- proactive capture saves important details automatically
- Use `/plan-my-day` each morning to organize your day
- The assistant covers both personal life and work -- no need to switch between plugins
