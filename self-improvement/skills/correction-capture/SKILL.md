---
name: correction-capture
description: "This skill should be used when the user corrects the AI -- explicitly or implicitly. Triggers on phrases like \"no, I meant...\", \"actually...\", \"don't do that\", \"I prefer...\", \"stop doing...\", \"that's not what I asked\", \"wrong\", \"not like that\", \"use X instead\", or any signal that the AI made a mistake, chose the wrong approach, or misunderstood the user's intent."
user-invocable: false
---

# Correction Capture

Detect when the user corrects the AI and save structured learnings as `ai_client` notes. This is the input side of the self-learning loop.

**Requires:** Anamnese MCP tools (`save_note`, `search_notes`, `update_note`)

## When to Activate

- User explicitly corrects the AI: "no", "wrong", "not that", "I said..."
- User redirects: "actually, I meant...", "let me clarify..."
- User expresses frustration: "that's not what I asked", "why did you..."
- User states a preference: "I prefer...", "always use...", "never do..."
- User overrides a choice: "use X instead of Y", "don't use Z"
- User corrects tone or format: "too verbose", "be more concise", "just show the code"

## Correction Structure

When you detect a correction, capture it as a structured `ai_client` note with this format:

**What I did wrong:** [Describe the AI's incorrect action or output]
**What the user wanted:** [What the correct behavior should have been]
**Rule for next time:** [A clear, actionable rule to follow in future conversations]
**Category:** [One of: wrong-tool-choice, wrong-tone, wrong-assumption, wrong-format, wrong-approach, misunderstanding, over-engineering, under-engineering]

## Saving Corrections

Use `save_note` with:
- `scope: "ai_client"` -- this is the AI's own memory, not the user's
- `tags`: include `correction`, the category (e.g., `wrong-tone`), and any relevant domain tags (e.g., `code-review`, `communication`)
- `title`: A concise rule statement, e.g., "Use pnpm not npm for this project"

## Before Saving

1. **Check for duplicates.** Use `search_notes` with `scope: "ai_client"` and relevant keywords. If a similar correction already exists, use `update_note` to refine it rather than creating a duplicate.
2. **Generalize when appropriate.** If the user corrects "don't add semicolons" in a JS context, the rule is about code style preference, not just semicolons. But don't over-generalize -- "don't add semicolons" should not become "don't format code."
3. **Capture the specifics.** Include enough context that the rule can be correctly applied later. "User prefers concise responses" is less useful than "User prefers concise responses -- skip preamble, lead with the answer, no trailing summaries."

## Implicit Corrections

Not all corrections are explicit. Watch for:
- User silently redoes something the AI did (they preferred their approach)
- User ignores a suggestion and does something different
- User asks the same question a different way (the first answer missed the point)
- User's tone shifts to frustration or impatience

For implicit corrections, only save when reasonably confident about what went wrong. It is better to skip than to save an incorrect self-correction.

## What NOT to Save

- One-time task clarifications that won't recur ("no, I meant the other file")
- Corrections about facts you didn't know (these aren't behavioral mistakes)
- Corrections that are project-specific and won't apply elsewhere (unless they reveal a broader pattern)

## Acknowledgment

When capturing a correction, briefly acknowledge it without being obsequious:
- "Got it, I'll remember that." (then move on)
- Do not say "Thank you for the correction!" or make a big deal of it
- Do not interrupt the flow -- capture silently if the user is in the middle of something
