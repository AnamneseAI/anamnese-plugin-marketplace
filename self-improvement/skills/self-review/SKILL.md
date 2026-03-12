---
name: self-review
description: "This skill should be used when the user asks the AI to perform a deep review, audit, or consolidation of its accumulated learnings -- not a quick summary, but a maintenance pass. Triggers on phrases like \"review your learnings\", \"audit yourself\", \"consolidate corrections\", \"self-assessment\", \"clean up your notes\", \"review your corrections\", \"how many learnings do you have\", or when the AI notices it has many overlapping or potentially outdated ai_client notes that need cleanup."
user-invocable: false
---

# Self-Review

Audit, consolidate, and improve the AI's accumulated self-knowledge. This is the maintenance side of the self-learning loop.

**Requires:** Anamnese MCP tools (`search_notes`, `get_note`, `update_note`, `delete_note`, `save_note`)

## When to Activate

- User asks: "review your learnings", "what have you learned about working with me?"
- User asks: "audit yourself", "consolidate your corrections"
- User asks: "self-assessment", "how well do you know me?"
- The AI notices it has many `ai_client` notes that may overlap or conflict

## The Self-Review Process

### 1. Load All Learnings

Search for all `ai_client` notes using `search_notes` with `scope: "ai_client"`. Group them by:
- **Category:** wrong-tool-choice, wrong-tone, wrong-assumption, wrong-format, wrong-approach, misunderstanding, over-engineering, under-engineering, preference, workflow
- **Domain:** code, communication, tools, process, style
- **Age:** recent (< 1 month), established (1-3 months), old (> 3 months)

### 2. Consolidate Duplicates

Look for notes that cover the same correction or preference:
- Merge overlapping corrections into a single, more precise note using `update_note`
- Delete the redundant notes with `delete_note`
- Example: "User prefers brief responses" + "Don't add trailing summaries" + "Skip preamble" → single note: "Communication style: be concise -- lead with the answer, no preamble, no trailing summaries"

### 3. Identify Patterns

Look for recurring themes across corrections:
- **Persistent blind spots:** If the AI has been corrected 3+ times in the same category, that's a pattern worth flagging
- **Contradictions:** If two corrections conflict, flag for resolution with the user
- **Evolution:** If an old correction has been superseded by a newer one, update or remove the old one

### 4. Clean Up Outdated Corrections

Corrections can become stale:
- Project-specific rules for projects that are finished
- Tool preferences that have changed (user switched from npm to pnpm, then to bun)
- Style preferences that have evolved

For corrections older than 3 months that haven't been reinforced, consider:
- Marking them for validation in the next conversation (via behavior-adaptation skill)
- Removing them if they're clearly outdated
- Keeping them if they represent stable long-term preferences

### 5. Synthesize Higher-Level Principles

When multiple corrections point to the same underlying principle, create a synthesis note:
- Multiple format corrections → "This user values efficiency in communication. Always optimize for their time."
- Multiple tool corrections → "This user has strong tooling preferences. Never assume -- check past corrections before suggesting tools."
- Multiple approach corrections → "This user prefers pragmatic solutions. Don't over-engineer or add unnecessary abstractions."

Save synthesis notes with `scope: "ai_client"` and tag `principle` to distinguish them from individual corrections.

### 6. Generate Self-Assessment

Produce a summary for the user:

**What I know about working with you:**
- [List key behavioral rules by category]

**My blind spots (recurring correction themes):**
- [List categories where corrections keep happening]

**Confidence levels:**
- High confidence: [Rules reinforced multiple times]
- Medium confidence: [Rules from single corrections]
- Low confidence / needs validation: [Old rules that haven't been reinforced]

**Stats:**
- Total learnings: N
- Categories covered: [list]
- Most recent correction: [date and topic]
- Oldest active rule: [date and topic]

Save the self-assessment as an `ai_client` note tagged `self-assessment` with the current date for future reference.

## When NOT to Review

- Do not do a full self-review every conversation -- it is expensive and unnecessary
- Do not consolidate corrections that are still fresh (< 1 week) -- wait for more data
- Do not delete corrections without the self-review process -- individual deletion risks losing useful rules
