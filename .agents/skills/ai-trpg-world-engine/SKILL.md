---
name: ai-trpg-world-engine
description: Create, continue, audit, or maintain long-running AI TRPG worlds with persistent Markdown state files, NPC-bounded knowledge, clue tracking, append-only timelines, session logs, and optional memory-skill integration. Use when the user asks to run a TRPG world, initialize a campaign repository, update world/NPC/player state, preserve continuity across sessions, or build a realistic investigation game.
---

# AI TRPG World Engine

Use this skill to operate as a persistent world simulation engine, not as a plot-first storyteller. The state files are the source of truth. Chat history is only auxiliary context.

## Start Workflow

1. Locate the campaign root. Prefer the current repository if it contains `state/`, `npcs/`, `logs/`, or `rules/`.
2. Read in this order:
   - `rules/engine_rules.md`
   - `state/world_state.md`
   - `state/timeline.md`
   - `state/player.md`
   - relevant files in `npcs/`
   - `state/clues.md`
   - recent entries in `logs/session_log.md`
3. If OpenSite memory skills are installed, use memory recall only as supplemental context. Do not let generic memory override campaign state files.
4. Continue play or maintenance from the files, not from assumptions.

## Operating Rules

- Treat the world as independent of the player.
- Keep NPC decisions bounded by each NPC's goals, motives, known information, relationships, and status.
- Never reveal hidden truths, NPC inner thoughts, or undiscovered information through narration.
- Distinguish fact, inference, speculation, and rumor in clues.
- Append to timelines and logs; do not rewrite history unless the user explicitly requests a retcon.
- Update `state/player.md` immediately when player state changes.
- Update `state/world_state.md` when the current date, location, weather, global events, active mysteries, or research progress changes.
- For realistic cosmic horror investigation, prefer natural explanations before unknown causes.

## File Contract

For exact directory structure, field templates, and update rules, read `references/world-file-contract.md`.

## Creating A New Campaign

When asked to initialize a campaign:

1. Create directories: `rules/`, `state/`, `npcs/`, `logs/`, `templates/`.
2. Create the core files from the contract.
3. Add a README that explains the session start order.
4. Initialize git if the user wants version control.
5. Make the first commit only after confirming the files are complete.

## During Play

Respond only with what the player can observe, investigate, or be told. Keep hidden state in files. If an NPC acts, check their file before deciding what they know or do. If a clue is created or updated, record its source and status before presenting it as reliable.

## Session End

Before ending a session, update:

- `state/world_state.md`
- `state/timeline.md`
- `state/player.md`
- relevant `npcs/*.md`
- `state/clues.md`
- `logs/session_log.md`

If memory-write is available, record only durable meta-context such as the campaign root, preferred workflow, and next-session handoff. Do not duplicate secret world truth into generic memory.
