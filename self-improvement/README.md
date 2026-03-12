# Self-Improvement

AI self-learning through corrections. The AI captures mistakes, adapts behavior from past corrections, and periodically consolidates learnings -- backed by persistent cloud memory.

## Getting Started

1. **Install the plugin** -- `claude plugins add self-improvement@anamnese-marketplace`
2. **Authenticate** -- Run `/start` or `/mcp` to sign in via browser
3. **Just work** -- The AI learns from your corrections automatically

## Commands

| Command | Description |
|---------|-------------|
| `/start` | Onboard, authenticate, and bootstrap your AI's self-knowledge |

## Skills (auto-activated)

| Skill | What it does |
|-------|-------------|
| Anamnese | Core memory, tasks, goals, notes, and proactive capture |
| Correction Capture | Detect when you correct the AI and save structured learnings |
| Behavior Adaptation | Load and apply past corrections at conversation start |
| Self-Review | Audit, consolidate, and clean up accumulated AI learnings |

## How It Works

The self-learning loop:

1. **Capture** -- When you correct the AI ("no, I meant...", "don't do that", "I prefer..."), the correction is captured as a structured learning with what went wrong, what you wanted, and the rule for next time
2. **Adapt** -- At the start of each conversation, the AI loads its past corrections and proactively applies them before making the same mistakes
3. **Review** -- Periodically, accumulated corrections are consolidated, duplicates merged, outdated rules cleaned up, and patterns identified

## The Concept

Every AI client starts as a blank slate. This plugin gives the AI persistent memory of its own mistakes. When you correct it, it remembers. Next conversation, it checks its corrections before acting. Over time, it becomes specifically tuned to how you work.

This is powered by Anamnese's `ai_client` scoped notes -- persistent memory that belongs to the AI, not the user.

## Integrations

- **Anamnese** -- Personal memory, tasks, goals, and notes

This plugin is minimal by design -- just Anamnese. No extra integrations to configure.

## License

MIT
