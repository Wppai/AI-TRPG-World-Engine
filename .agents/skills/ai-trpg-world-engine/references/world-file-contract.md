# World File Contract

## Directory Structure

```text
campaign-root/
  rules/
    engine_rules.md
  saves/
    active_save.md
    _template/
      save.md
      state/
        world_state.md
        timeline.md
        player.md
        clues.md
      npcs/
        .gitkeep
      logs/
        session_log.md
    <save-name>/
      save.md
      state/
        world_state.md
        timeline.md
        player.md
        clues.md
      npcs/
        npc_<name>.md
      logs/
        session_log.md
  templates/
    npc_template.md
```

`rules/`, `templates/`, and `.agents/skills/` are the reusable engine base. `saves/<save-name>/` is the story-specific source of truth.

## active_save.md

Track which save is currently in use:

```markdown
# Active Save

Current Save:
ghost-island

Notes:
- Change `Current Save` when starting or resuming a different story.
- Do not point this to `_template`.
```

## save.md

Each save must include metadata:

```markdown
# Save Metadata

Name:

Slug:

Status:
Draft | Active | Completed | Archived

Created:

Completed:

Description:

Notes:
- 
```

When a story ends, set `Status: Completed`, fill `Completed`, and leave the save intact.

## world_state.md

Required fields:

```markdown
# World State

Current Date:

Current Location:

Weather:

Global Events:
- 

Research Progress:
- 

Active Mysteries:
- 
```

Write world-level changes here. Do not use this file as a transcript.

## timeline.md

Use append-only dated entries:

```markdown
YYYY-MM-DD
- Event one.
- Event two.
```

The timeline is the world's historical truth. Preserve previous entries.

## clues.md

Use this structure:

```markdown
Clue:

Source:

Status:
Verified | Possible | False

Type:
Fact | Inference | Speculation | Rumor

Related Events:

Notes:
```

Never promote an inference, speculation, or rumor into fact without investigation.

## player.md

Track:

```markdown
Name:

Location:

Money:

Equipment:
- 

Health:

Relationships:
- 

Tasks:
- 

Research Progress:
- 

Known Information:
- 
```

The player can only act on known information recorded here or newly obtained in play.

## NPC Files

Use one file per NPC:

```markdown
# NPC: Name

Name:

Status:
Alive

Occupation:

Goal:

Motivation:

Known:
- 

Unknown:
- 

Position:

Relationship:
- 

Personality:
- 

State Notes:
- 
```

When an NPC dies, set `Status: Dead`. Do not delete the file.

## session_log.md

Record only what happened:

```markdown
YYYY-MM-DD
- The player visited the archive.
- The clerk refused access.
```

Do not log hidden truth, NPC inner thoughts, or GM-only explanations.
