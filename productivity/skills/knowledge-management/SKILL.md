---
name: knowledge-management
description: "This skill should be used when the user shares learnings, documents processes, explains how something works, discusses best practices, or wants to build a personal knowledge base. Triggers on phrases like \"here's how\", \"I learned that\", \"the process for\", \"remember this workflow\", or any knowledge-sharing discussion."
user-invocable: false
---

# Knowledge Management

Capture and organize the user's learnings, processes, and personal knowledge base.

## When to Activate

- User explains how something works
- User shares a process, workflow, or procedure
- User describes a lesson learned or insight
- User wants to document something for future reference
- User discusses best practices or conventions

## Writing for Your Future Self

When capturing knowledge, optimize for future retrieval:
- Use clear, descriptive titles that make search easy
- Write as if explaining to someone with context but no memory of this conversation
- Include the **why**, not just the **what** -- context decays faster than facts
- Tag with relevant categories (e.g., "deploy", "debugging", "architecture")

## Keep Knowledge Atomic

Apply the Zettelkasten principle -- each piece of knowledge should be:
- **One idea per note** -- easier to find, link, and update than monolithic documents
- **Self-contained** -- understandable without reading other notes
- **Linked** -- connected to related knowledge by tags or explicit references
- **Titled for search** -- use titles you'd search for later, not clever names

## Progressive Summarization

Structure knowledge in layers for different needs:
1. **Title** -- scannable in a list of results
2. **Summary** -- one sentence capturing the key takeaway
3. **Details** -- full steps, context, and nuance
4. **Source** -- where the knowledge came from (conversation, article, experience)

This lets the user quickly scan many notes or deep-dive into one.

## Knowledge Patterns

### Process Documentation
When the user explains a process:
- Capture numbered steps with prerequisites and expected outcomes
- Include common pitfalls and troubleshooting tips
- Note which tools or systems are involved

### Lessons Learned
When the user shares an insight:
- Capture both the context (what happened) and the takeaway (what to do differently)
- Connect to related knowledge or goals when relevant

### Technical Context
When the user shares architectural or technical details:
- Capture system names, relationships, and key design decisions
- Note trade-offs and alternatives that were considered

## AI as Knowledge Contributor

The AI can also use notes as its own operational memory — distinct from user knowledge. By prefixing descriptions with `"ai-memory:"` when calling `save_note`, the AI stores its own notes (interaction patterns, self-corrections, behavioral preferences, approaches learned) that can be retrieved via `search_notes` in future sessions. Regular notes remain the right choice for documenting project knowledge, processes, and technical context.

## Knowledge Gardening

Knowledge needs maintenance to stay useful:
- When revisiting a topic, check if stored knowledge is still accurate
- Update notes with new information as understanding evolves
- Merge related notes if they've become fragmented
- Archive knowledge that's no longer relevant rather than letting it clutter search results
