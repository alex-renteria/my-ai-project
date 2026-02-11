# Entire CLI

Entire is a developer platform that hooks into your git workflow to capture AI agent sessions on every push, unifying your code with its context and reasoning.

## Key Concepts

**Sessions**: Complete interactions with your AI agent from start to finish, capturing all prompts, responses, modified files, and timestamps. Format: `YYYY-MM-DD-<UUID>`.

**Checkpoints (Rewind Points)**: Snapshots within a session -- "save points" in your work. Checkpoint IDs are 12-character hex strings (e.g., `a3b2c4d5e6f7`). Stored on the `entire/checkpoints/v1` branch, separate from your code commits.

## Checkpoint Strategies

| Strategy | Behavior | Main Branch Safe? |
|----------|----------|-------------------|
| `manual-commit` | Triggered on git commit | Yes |
| `auto-commit` | Triggered after each agent response | Use with caution |

## Commands

| Command | Purpose |
|---------|---------|
| `entire enable` | Activate Entire in your repository |
| `entire status` | Display current session and strategy info |
| `entire rewind` | Select and restore to a previous checkpoint |
| `entire resume <branch>` | Restore session metadata for a branch |
| `entire disable` | Remove Entire hooks |
| `entire reset` | Delete shadow branch and session state |
| `entire doctor` | Fix or clean up stuck sessions |
| `entire explain` | Explain a session or commit |
| `entire clean` | Remove orphaned data |
| `entire version` | Display CLI version |

## Enable Flags

- `--strategy <name>`: `manual-commit` (default) or `auto-commit`
- `--agent <name>`: `claude-code` (default) or `gemini`
- `--force` / `-f`: Force reinstall hooks
- `--local`: Save settings to local file instead of project-wide
- `--skip-push-sessions`: Disable automatic pushing of session logs
- `--telemetry=false`: Opt out of usage analytics

## Configuration

Settings live in `.entire/settings.json` (committed) and `.entire/settings.local.json` (gitignored).

| Option | Values | Purpose |
|--------|--------|---------|
| `enabled` | true/false | Toggle Entire on/off |
| `log_level` | debug, info, warn, error | Logging verbosity |
| `strategy` | manual-commit, auto-commit | When to capture checkpoints |
| `strategy_options.push_sessions` | true/false | Auto-push checkpoint branch |
| `strategy_options.summarize.enabled` | true/false | Auto-generate AI summaries |
| `telemetry` | true/false | Send anonymous usage data |

## Requirements

- Git
- macOS or Linux (Windows via WSL)
- Claude Code or Gemini CLI installed and authenticated
