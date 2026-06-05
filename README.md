# AI TRPG World Engine

Long-running AI TRPG world simulation and state management system.

This repository is designed to preserve a persistent, logically consistent TRPG world. The files in this repository are the source of truth for the simulation. Chat history is only auxiliary context.

## Directory Structure

- `rules/`: engine rules and operating principles.
- `state/`: current world, player, timeline, and clue state.
- `npcs/`: one file per NPC.
- `logs/`: session records of what happened in play.
- `templates/`: reusable templates for new entities.

## Session Start Order

Read in this order before continuing play:

1. `rules/engine_rules.md`
2. `state/world_state.md`
3. `state/timeline.md`
4. `state/player.md`
5. Relevant files in `npcs/`
6. `state/clues.md`
7. Recent entries in `logs/session_log.md`

## Maintenance Rules

- Append to `state/timeline.md`; do not rewrite history.
- Update `state/world_state.md` when the current world changes.
- Update `state/player.md` whenever player state changes.
- Keep NPC knowledge bounded by each NPC file.
- Keep clues separated as fact, inference, speculation, or rumor.
- Record only observed events in `logs/session_log.md`.

## Citation

If you use this project in research, writing, derivative tools, or public non-commercial work, please cite it using `CITATION.cff`.
