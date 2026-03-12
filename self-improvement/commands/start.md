---
description: Onboard and authenticate with Anamnese, and bootstrap the AI's self-knowledge
---

Follow these steps to set up the AI self-learning system:

## Step 1: Authenticate

Call `get_user_profile` to check if Anamnese is authenticated.

- **If it returns a 401 or auth error:** Tell the user to run `/mcp` to authenticate via browser, then try again.
- **If it succeeds:** Continue to Step 2.

## Step 2: Check Anamnese MCP

Verify the Anamnese MCP is working by confirming the profile loaded successfully. This plugin only uses Anamnese -- no other integrations to configure.

## Step 3: Load Existing Self-Knowledge

Search for existing `ai_client` notes using `search_notes` with `scope: "ai_client"`.

**If notes exist:** Show the user a summary of the AI's current self-knowledge:
- How many corrections/learnings are stored
- Key categories (wrong tool choice, wrong tone, wrong assumption, wrong format, wrong approach)
- Most recent corrections

Say something like: "I already have N learnings from past conversations. Here's what I know about working with you: ..."

**If no notes exist (or very few):** Continue to Step 4.

## Step 4: Explain the Concept

If the AI has sparse self-knowledge, explain how the system works:

"I learn from my mistakes. When you correct me -- saying things like 'no, I meant...', 'don't do that', or 'I prefer...' -- I capture that correction and remember it. Next time we talk, I check my past corrections before acting, so I don't repeat the same mistakes.

Over time, I become specifically tuned to how you like to work."

Then ask: **"What are the most important things I should know about how you like to work?"**

Listen for preferences about:
- Communication style (brief vs detailed, formal vs casual)
- Tool preferences (specific languages, frameworks, tools)
- Workflow patterns (how they like to review code, make decisions, etc.)
- Pet peeves (things that frustrate them about AI assistants)

Save each answer as an `ai_client` note using `save_note` with `scope: "ai_client"` and descriptive tags like `preference`, `workflow`, `communication`, etc.

Don't ask all questions at once. Have a natural conversation, 2-3 questions at a time, and save as you go.

## Step 5: Orientation

Show the user what's available:

**Skills (activate automatically as you chat):**
- **Correction Capture** -- When you correct me, I save a structured learning: what I did wrong, what you wanted, and the rule for next time
- **Behavior Adaptation** -- At the start of each conversation, I load my past corrections and apply them proactively
- **Self-Review** -- Periodically I audit my learnings: consolidate duplicates, identify blind spots, clean up outdated rules

**How to get the most out of it:**
- Just correct me naturally when I get something wrong -- I'll capture it automatically
- Say "what do you know about working with me?" to see my current self-knowledge
- Say "review your learnings" to trigger a self-audit and cleanup
- The more you correct me, the better I get. Don't hold back.
