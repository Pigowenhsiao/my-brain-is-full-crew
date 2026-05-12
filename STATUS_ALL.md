# STATUS_2026-05-12_upstream_merge_codex_runtime

## What changes were made
- Fetched `https://github.com/gnekt/My-Brain-Is-Full-Crew.git` as `upstream` and merged `upstream/main` into the local `Codex` branch.
- Brought in the upstream multi-platform adapter architecture, Codex CLI adapter, vault mapping docs, orchestra helpers, contact-sync skill, MCP source config, updated scripts, updated docs, updated core agents/skills, and new regression/unit tests.
- Preserved local custom units by keeping `agents/note-update.md`, `agents/llm-wiki.md`, `skills/note-update/`, and `skills/concept-hub-navigation/`, then re-registering `note-update` and `llm-wiki` in `references/agents-registry.md` and `references/agents.md`.
- Kept local ignore rules for `.codex/settings.local.json` and `.gstack/`.
- Fixed Codex MCP TOML generation so names with spaces are emitted as quoted TOML tables, and restored `Google Calendar` in `mcp/servers.yaml`.
- Updated Codex adapter tests to expect this fork's extra custom agents and skills.

## Whether verification succeeded or failed
- Succeeded: `tests/adapters/codex-cli/adapter.test.sh` full function suite passed.
- Succeeded: `tests/scripts/codex-cli-install.test.sh` full function suite passed.
- Succeeded: `scripts/build.sh --platform codex-cli` completed successfully through Git Bash.
- Succeeded: `git diff --cached --check` passed.
- Failed: full `tests/run.sh` did not fully pass in this Windows environment.

## If verification still failed, the failure reason and blocker
- Full suite failure is blocked by missing `jq` on PATH. The failing tests are for Claude Code, Gemini CLI, and OpenCode JSON adapter/config validation, plus platform matrix checks that require `jq`.
- Earlier Codex-specific failures caused by custom fork inventory were fixed and retested successfully.

## What the next step should be
- Install or provide `jq` for Git Bash, then rerun `tests/run.sh` to verify the non-Codex adapters.
- Continue with commit and push for the Codex-verified upstream merge.
