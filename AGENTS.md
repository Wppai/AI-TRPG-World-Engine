# AGENTS.md

ATWE Version: v1.1

## Operation Modes

- FULL Mode: use when first taking over a save, auditing continuity, repairing drift, or when the user asks for full reload.
- LITE Mode: use during ordinary play to reduce token usage.
- Lite Day-Cycle: run a game day in LITE Mode, fully update the active save at day end, then reload core files at the start of the next game day.

## Token Budget Rules

- In LITE Mode, do not read the entire save unless explicitly requested.
- In FULL Mode, perform a controlled full read of the active save only.
- Always start from saves/active_save.md.
- In LITE Mode, read only:
  1. rules/engine_rules.md
  2. save.md
  3. world_state.md
  4. player.md
  5. timeline.md last 30 entries
  6. clues.md only relevant sections
  7. NPC files only for NPCs present in the scene
  8. session_log.md last 3 sessions

## Never Load By Default

- Full session_log.md
- All NPC files
- All historical clues
- All archived saves

## Update Policy

- Append timeline.
- Update only changed NPC files.
- Update only changed clue entries.
- Keep summaries short.
