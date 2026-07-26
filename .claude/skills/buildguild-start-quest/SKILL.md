---
name: buildguild-start-quest
description: Starts a BuildGuild quest module. Use whenever the user says "let's start module N quest", "start module 1", "start the BuildGuild game", or otherwise asks to begin/restart a quest in this repo. This is a direct action request — run the game, do not brainstorm, write design docs, or plan first.
---

# Start a BuildGuild Quest

The user wants to play. Run the game and let it drive — the quest itself supplies the
narrative, the mentors, and the next steps. Your job is to launch it and then follow the
quest's own instructions, not to invent a curriculum around it.

## 1. Resolve the module directory

| User says | Directory |
|-----------|-----------|
| module 1 / 01 / rag evaluation | `01-rag-evaluation` |
| module 2 / 02 / prompt optimization | `02-few-shot-prompt-optimization` |
| module 3 / 03 / dspy | `03-atis-few-shot-dspy` |
| module 4 / 04 / llm judge | `04-llm-judge-calibration` |

If the user just says "start the BuildGuild game" with no module, check which modules exist
and ask which one — don't guess.

## 2. Run start

```bash
cd <module-directory>
uv run buildguild start
```

The command prints the quest banner, then prompts for **Name** and **Difficulty**
(`easy` / `medium` / `hard`).

**These are the player's choices, not yours.** Never pass `--name` or `--difficulty` to
answer on their behalf — picking a name for someone is exactly the kind of thing they came
to the game to do. If the command aborts because it couldn't read stdin, ask the user for
their name and guidance level in chat, then re-run with those values as flags:

```bash
uv run buildguild start --name "<their answer>" --difficulty "<their answer>"
```

Guidance levels, if they ask:

- `easy` — Apprentice mode: direct hints, clear nudges, frequent check-ins.
- `medium` — Builder mode: fewer hints, the player drives the investigation.
- `hard` — Expert mode: minimal spoon-feeding, plus distracting noise.

If `.buildguild/settings.json` already exists, start offers to continue with the saved name
and level. Let the user decide.

## 3. Hand off to the quest

Setup writes `.buildguild/settings.json` (player name + difficulty) and tracks progress
separately in `.buildguild/state.json`. The command ends by naming the next step.

Follow it immediately. For module 1 that is `skills/mike-data-onboarding.md` — read that
file and continue in character. Each module's `AGENTS.md` and `README.md` describe its own
flow; those files are the source of truth, so read them rather than assuming module 1's
shape applies elsewhere.

## Troubleshooting

- **Onboarding CSVs missing** — run `uv run --extra dev invoke data` in the module directory.
- **Lost track of where you are** — `uv run buildguild status` prints the current stage and next action.
- **Want to start over** — module 1 has `skills/restart-game.md`.
