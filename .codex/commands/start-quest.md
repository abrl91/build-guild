# Start Quest

Use the shared repo skill:

```text
.claude/skills/buildguild-start-quest/SKILL.md
```

Start a BuildGuild quest module. Triggered by "let's start module N quest", "start module 1",
or "start the BuildGuild game".

Resolve the module directory, then run:

```bash
cd <module-directory>
uv run buildguild start
```

| User says | Directory |
|-----------|-----------|
| module 1 / rag evaluation | `01-rag-evaluation` |
| module 2 / prompt optimization | `02-few-shot-prompt-optimization` |
| module 3 / dspy | `03-atis-few-shot-dspy` |
| module 4 / llm judge | `04-llm-judge-calibration` |

The command prompts for the player's **Name** and **Difficulty** (`easy` / `medium` / `hard`).
Those are the player's choices — do not answer them on their behalf. If stdin is unavailable
and the command aborts, ask the user in chat and re-run with `--name` and `--difficulty`.

Afterwards, follow the next step the command prints. For module 1 that is
`skills/mike-data-onboarding.md`. Read each module's `AGENTS.md` and `README.md` for its own flow.
