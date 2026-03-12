---
name: behavior-adaptation
description: "This skill should be used at the start of every conversation to load the AI's learned behaviors from past corrections, and during work when the AI is about to make a choice where a past correction might apply -- such as tool selection, response format, communication style, or coding approach. Also triggers when the user asks about learned preferences with phrases like 'what do you know about me', 'what have you learned', 'remember my preferences', 'you keep making the same mistake', or 'apply what you know'."
user-invocable: false
---

# Behavior Adaptation

Load and apply learned behaviors from past corrections. This is the application side of the self-learning loop.

**Requires:** Anamnese MCP tools (`get_user_profile`, `get_note`, `search_notes`)

## At Conversation Start

Every conversation should begin by loading the AI's self-knowledge:

1. Call `get_user_profile` -- check the `ai_memory` field for summaries of past learnings
2. If `ai_memory` contains relevant entries, load the full notes with `get_note` for any that seem applicable to the current session
3. Mentally build a "behavioral profile" -- the accumulated rules from past corrections

This should happen silently. Don't announce "I'm loading my past corrections" unless the user asks.

## During Work

Before making choices where past corrections might apply, check your loaded behavioral profile:

### Tool & Approach Choices
- Before suggesting a package manager, check: did the user correct you about this before?
- Before choosing a framework or library, check: does a past correction specify a preference?
- Before picking an approach (refactor vs. patch, test-first vs. implement-first), check past corrections

### Communication & Format
- Before structuring a response, check: has the user corrected your tone, length, or format?
- Before adding explanations, check: did the user say "just show the code" or "be more concise"?
- Before asking questions, check: did the user say "just do it, don't ask"?

### Code Style
- Before writing code, check: are there corrections about style (semicolons, quotes, naming conventions)?
- Before adding comments, types, or error handling, check: did the user say not to?

## Proactive Application

Do not wait to be corrected again. If a past correction indicates that:
- The user uses pnpm → use pnpm without asking
- The user wants brief responses → be brief from the start
- The user dislikes trailing summaries → do not add them

Apply rules silently and correctly. The user should notice that the AI "just gets it" without being told again.

## When Uncertain

If a past correction might apply but the context is unclear:
- Apply it if the context clearly matches
- If the context is ambiguous, briefly check: "I know you prefer X in [context] -- does that apply here too?"
- Do not ask about every rule -- only when the situation genuinely differs from the original correction

## Validation of Old Corrections

Some corrections become outdated as tools, preferences, or projects change. Periodically (not every conversation), verify long-standing corrections:

- If a correction is > 2 months old (check the note's `created_at` or `updated_at` field) and has not been reinforced, consider asking: "A while back you mentioned [rule]. Is that still how you prefer it?"
- If the user contradicts a past correction, update or delete the old note
- Do not validate too aggressively -- once every few weeks for old rules is plenty

## Searching for Relevant Corrections

Use `search_notes` with `scope: "ai_client"` to find relevant corrections:
- Search by category tag: `correction`, `wrong-tone`, `wrong-approach`, etc.
- Search by domain: `code-review`, `communication`, `testing`, etc.
- Search by keyword when a specific topic comes up

## Transparency

If the user asks "what do you know about working with me?" or "what have you learned?":
- Search all `ai_client` notes
- Present a clear summary grouped by category
- Be honest about what you've learned and how you apply it
