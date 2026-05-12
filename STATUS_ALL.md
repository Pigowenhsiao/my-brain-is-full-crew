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

# STATUS_2026-05-12_upstream_merge_pushed

## What changes were made
- Created commit `f521808` with the upstream runtime merge, Codex-specific fixes, fork custom-agent preservation, tests, and status log.
- Pushed branch `Codex` to `origin` at `https://github.com/Pigowenhsiao/my-brain-is-full-crew.git`.

## Whether verification succeeded or failed
- Succeeded: git commit completed.
- Succeeded: git push completed.
- Previous verification remains: Codex adapter tests passed, Codex install/update tests passed, Codex build passed, and staged diff check passed before the merge commit.
- Full cross-platform test suite still failed because `jq` is missing from the local Git Bash environment.

## If verification still failed, the failure reason and blocker
- The remaining blocker is environmental: install `jq` for Git Bash to run Claude Code, Gemini CLI, and OpenCode JSON adapter tests.

## What the next step should be
- Install `jq`, rerun `tests/run.sh`, and commit any resulting non-Codex adapter fixes only if the rerun exposes code issues rather than environment issues.

# STATUS_2026-05-12_codex_dispatcher_refusion

## What changes were made
- Rechecked the upstream merge for Codex usability and found that root `AGENTS.md` was still the old Codex-only dispatcher.
- Updated `DISPATCHER.md` to include this fork's 16 skills and 8 core + 2 custom agent inventory.
- Added `/note-update` and `/concept-hub-navigation` to the shared skill registry and agent directory references.
- Tightened `adapters/codex-cli/adapter.sh` so generated Codex output removes stale `Skill tool`, `Agent tool`, `.mcp.json`, `.platform`, `.codex/skills`, and max-depth-3 wording.
- Rebuilt Codex output and synchronized the generated Codex `AGENTS.md` back to the repo root.

## Whether verification succeeded or failed
- Succeeded: Codex build completed with `scripts/build.sh --platform codex-cli`.
- Succeeded: root `AGENTS.md` scan found the required Codex/fork signals: `CODEX-ROUTING-HEADER`, 16 skills, 8 core + 2 custom agents, `.agents/skills`, `.codex/agents`, `.codex/config.toml`, `note-update`, and `concept-hub-navigation`.
- Succeeded: root `AGENTS.md` scan found no major Codex incompatibility residues for `.platform`, `.mcp.json`, `.codex/skills`, `Skill tool`, `Agent tool`, `AskUserQuestion`, `request_user_input`, `Max depth 3`, or stale `.codex/agents/{name}.md`.
- Succeeded: full Codex adapter test function suite passed.
- Succeeded: Codex install/update test function suite passed.
- Succeeded: `git diff --check` passed.

## If verification still failed, the failure reason and blocker
- Full cross-platform `tests/run.sh` remains blocked by missing `jq` in the local Git Bash environment for Claude Code, Gemini CLI, and OpenCode JSON adapter tests.

## What the next step should be
- Commit and push the Codex dispatcher refusion.
- Install `jq` later if full non-Codex platform verification is required.

# STATUS_2026-05-12_codex_dispatcher_refusion_pushed

## What changes were made
- Created commit `735253f` for the Codex dispatcher refusion.
- Pushed branch `Codex` to `origin` after aligning root `AGENTS.md`, source `DISPATCHER.md`, Codex adapter normalization, and shared registries.

## Whether verification succeeded or failed
- Succeeded: commit completed.
- Succeeded: push completed.
- Verification before commit succeeded for Codex adapter tests, Codex install/update tests, Codex build, root `AGENTS.md` compatibility scans, and diff checks.

## If verification still failed, the failure reason and blocker
- No Codex-specific blocker remains.
- Full non-Codex adapter verification still requires `jq` on PATH.

## What the next step should be
- Optional: install `jq` and rerun `tests/run.sh` for full Claude/Gemini/OpenCode adapter coverage.
