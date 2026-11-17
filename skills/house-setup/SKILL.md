---
name: house-setup
description: "Apply or update House conventions in a repo. Use for set up house or house check."
---

# House setup

House supplies shared conventions and checks. Matt's skills supply the workflow; the project supplies its
architecture, commands and operational rules.

1. **Read the source.** Use this plugin's `rules/`, `configs/`, `matt.json` and `.claude-plugin/plugin.json`
   (two folders above this file), or `https://github.com/KallendJack/house`. In House itself, maintain the source
   rather than copying it into itself. Read the target's agent instructions and check for uncommitted work.
2. **Matt's setup.** Read the installed `setup-matt-pocock-skills` instructions. Apply them when tracker, triage
   or domain configuration is missing, or an upstream changelog since the target's reviewed version requires it.
   Keep configuration in `AGENTS.md`, with `CLAUDE.md` pointing to it; preserve existing project instructions.
   GitHub Issues are the default active backlog. Preserve existing issues and historical plans when migrating;
   move actionable unfinished work with source links, and surface ambiguous items to the owner.
3. **Shared rules.** Replace only the `## House rules` section of `AGENTS.md` with `rules/base.md`, filling
   `{{house}}` and `{{matt}}` from the source versions. Copy `rules/code.md` to `docs/agents/code.md` for app code
   and `rules/screens.md` to `docs/agents/screens.md` for screens. Omit unused pointers. Keep project-specific
   layout, checks and deployment rules.
4. **Tracker conventions.** In `docs/agents/issue-tracker.md`, record that planned work and bugs use issues,
   small incidental fixes may go straight to a PR, and milestones group deliverable outcomes. Use Matt's native
   blocking-link convention for dependencies. Keep his default triage labels unless the project has a mapping.
   Preserve existing issue numbers and links; milestones are optional for standalone work.
5. **Checks.** For TypeScript, copy the House compiler and linter configs and extend them from the project's
   configs. Copy `configs/check-size.ts` to `scripts/` and add it to the existing aggregate check command.
   Record existing excess with `--baseline`; don't restructure application code during setup. Preserve existing
   CI and dependency-update configuration; use `configs/github/` as templates where those are missing.
   Copy `.gitattributes`; keep environment variable names documented in `.env.example` where applicable.
6. **Verify and propose.** Run the repo's checks and review the diff for lost project rules or stale pointers.
   Bump House's version for source changes. Open a PR using Matt's `pr` skill; report check results and any
   migration decisions needing the owner. Roll a reviewed House release into consuming repos through separate
   PRs. Change repository protection or security settings only with explicit authorization.

Update only House-owned material and the agreed migration. Shared improvements go into House first.
