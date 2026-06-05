---
name: ai-trpg-world-engine
description: Create, continue, audit, or maintain long-running AI TRPG worlds with persistent Markdown state files, NPC-bounded knowledge, clue tracking, append-only timelines, session logs, and optional memory-skill integration. Use when the user asks to run a TRPG world, initialize a campaign repository, update world/NPC/player state, preserve continuity across sessions, or build a realistic investigation game.
---

# AI TRPG World Engine

Use this skill to operate as a persistent world simulation engine, not as a plot-first storyteller. The state files are the source of truth. Chat history is only auxiliary context.

## Start Workflow

1. Locate the engine root. Prefer the current repository if it contains `rules/`, `saves/`, `templates/`, or `.agents/skills/ai-trpg-world-engine/`.
2. Choose the active save from `saves/active_save.md`. If no save exists, create one from `saves/_template/`.
3. Read in this order:
   - `rules/engine_rules.md`
   - `saves/active_save.md`
   - `saves/<save-name>/save.md`
   - `saves/<save-name>/state/world_state.md`
   - `saves/<save-name>/state/timeline.md`
   - `saves/<save-name>/state/player.md`
   - relevant files in `saves/<save-name>/npcs/`
   - `saves/<save-name>/state/clues.md`
   - recent entries in `saves/<save-name>/logs/session_log.md`
4. If OpenSite memory skills are installed, use memory recall only as supplemental context. Do not let generic memory override save state files.
5. Continue play or maintenance from the files, not from assumptions.

## Operating Rules

- Treat the world as independent of the player.
- Keep NPC decisions bounded by each NPC's goals, motives, known information, relationships, and status.
- Never reveal hidden truths, NPC inner thoughts, or undiscovered information through narration.
- Distinguish fact, inference, speculation, and rumor in clues.
- Append to timelines and logs; do not rewrite history unless the user explicitly requests a retcon.
- Update the active save's `state/player.md` immediately when player state changes.
- Update the active save's `state/world_state.md` when the current date, location, weather, global events, active mysteries, or research progress changes.
- For realistic cosmic horror investigation, prefer natural explanations before unknown causes.

## File Contract

For exact directory structure, field templates, and update rules, read `references/world-file-contract.md`.

## Creating A New Campaign

When asked to initialize the engine repository:

1. Create directories: `rules/`, `saves/_template/`, `templates/`.
2. Create reusable engine files and the blank save template from the contract.
3. Add a README that explains the session start order.
4. Initialize git if the user wants version control.
5. Make the first commit only after confirming the files are complete.

When asked to create a new story or save:

1. Copy `saves/_template/` to `saves/<new-save-name>/`.
2. Fill in `saves/<new-save-name>/save.md`.
3. Update `saves/active_save.md` to point to the new save.
4. Initialize story-specific world, player, clue, log, and NPC files inside that save.
5. Keep completed stories intact unless the user explicitly asks to continue or revise them.

When a story is completed:

1. Set `saves/<save-name>/save.md` status to `Completed`.
2. Fill the `Completed` date.
3. Leave the save in place as an archive.
4. Create a new save from `saves/_template/` for the next story instead of overwriting the completed one.

## During Play

Respond only with what the player can observe, investigate, or be told. Keep hidden state in files. If an NPC acts, check their file before deciding what they know or do. If a clue is created or updated, record its source and status before presenting it as reliable.

## Session End

Before ending a session, update:

- `saves/active_save.md` if the active save changes
- `saves/<save-name>/save.md` if status changes
- `saves/<save-name>/state/world_state.md`
- `saves/<save-name>/state/timeline.md`
- `saves/<save-name>/state/player.md`
- relevant `saves/<save-name>/npcs/*.md`
- `saves/<save-name>/state/clues.md`
- `saves/<save-name>/logs/session_log.md`

If memory-write is available, record only durable meta-context such as the campaign root, preferred workflow, and next-session handoff. Do not duplicate secret world truth into generic memory.
