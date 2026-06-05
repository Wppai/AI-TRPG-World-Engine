# AI TRPG World Engine

Long-running AI TRPG world simulation and state management system.

This repository is designed to preserve persistent, logically consistent TRPG worlds. The engine files define the reusable operating rules, while each save under `saves/` contains the source of truth for one story or campaign. Chat history is only auxiliary context.

## Directory Structure

- `rules/`: reusable engine rules and operating principles.
- `saves/`: story/campaign saves.
- `saves/active_save.example.md`: example active-save pointer.
- `saves/active_save.md`: local pointer to the currently active save, ignored by Git.
- `saves/_template/`: blank save template for new stories.
- `saves/<save-name>/`: local story save, ignored by Git by default.
- `saves/<save-name>/save.md`: metadata for one save, including status.
- `saves/<save-name>/state/`: current world, player, timeline, and clue state for one save.
- `saves/<save-name>/npcs/`: one file per NPC in that save.
- `saves/<save-name>/logs/`: session records for that save.
- `templates/`: reusable templates for new entities.

## Session Start Order

Choose one active save from `saves/active_save.md`, then read in this order before continuing play:

1. `rules/engine_rules.md`
2. `saves/<save-name>/save.md`
3. `saves/<save-name>/state/world_state.md`
4. `saves/<save-name>/state/timeline.md`
5. `saves/<save-name>/state/player.md`
6. Relevant files in `saves/<save-name>/npcs/`
7. `saves/<save-name>/state/clues.md`
8. Recent entries in `saves/<save-name>/logs/session_log.md`

## Creating A New Save

Copy `saves/_template/` to `saves/<new-save-name>/`, copy `saves/active_save.example.md` to `saves/active_save.md`, fill in `saves/<new-save-name>/save.md`, and update `saves/active_save.md`. Real saves are ignored by Git by default so public repositories can share the engine without leaking story state.

Recommended branch workflow:

```powershell
git checkout main
git pull
git checkout -b story/<new-save-name>
```

Keep `main` as the reusable engine base. Use `story/<save-name>` branches for running or experimenting with individual stories. Because real saves are ignored by Git, they stay local unless you explicitly force-add them for a private branch or private remote.

To version a save intentionally:

```powershell
git add -f saves/active_save.md saves/<save-name>/
git commit -m "Add <save-name> story save"
```

Do this only for private repositories or branches you are comfortable exposing.

## Maintenance Rules

- Append to the active save's `state/timeline.md`; do not rewrite history.
- Update the active save's `state/world_state.md` when the current world changes.
- Update the active save's `state/player.md` whenever player state changes.
- Keep NPC knowledge bounded by each NPC file.
- Keep clues separated as fact, inference, speculation, or rumor.
- Record only observed events in the active save's `logs/session_log.md`.

## Citation

If you use this project in research, writing, derivative tools, or public non-commercial work, please cite it using `CITATION.cff`.
