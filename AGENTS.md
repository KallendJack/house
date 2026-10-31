# house

The house standard: the rules, configs and skills every repo follows, whatever the project. Project rules stay in
each project's own `AGENTS.md`.

## What's here

- `rules/base.md`: the `## House rules` section every repo's `AGENTS.md` carries.
- `rules/code.md`, `rules/screens.md`: the extras, copied to a repo's `docs/agents/` when it has app code or screens.
- `configs/`: `tsconfig.house.json`, `biome.house.json`, the size check (`check-size.ts`, with its test),
  `.gitattributes`, and `github/` (CI and Dependabot templates).
- `skills/`: `house-setup` (write the standard into a repo or update it) and `lead` (keep a repo's work moving).
- `.claude-plugin/`: the marketplace and plugin manifests that Claude Code and Codex install from.

## Rules for this repo

- **Matt Pocock's skills come first.** Where his skills have a rule, it wins; this repo only fills gaps. When he adds
  or changes something that covers a rule here, drop ours.
- **General only.** Nothing specific to one project, and nothing about the owner, their places or their plans: the
  repo is public.
- **Short.** Every line here becomes an order an agent follows in every repo. Cut before adding.
- **Concepts, not a stack.** Rules say what to do in words any stack can follow, with how TypeScript does it.
- **A change here is a change everywhere:** bump `version` in `.claude-plugin/plugin.json`, and run `house-setup` in
  the repos it affects.
- Check: `node --test configs/check-size.test.ts`.
