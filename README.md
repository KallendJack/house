# house

The rules, configs and skills every one of my repos follows, whatever the project, on top of
[Matt Pocock's skills](https://github.com/mattpocock/skills).

- **Rules:** a short base for every repo's `AGENTS.md`, plus extras for app code and screens.
- **Configs:** strict TypeScript, Biome, and a size check (400 lines a file, 15 files a folder).
- **Skills:** `house-setup` writes the standard into a repo or brings it up to date.

## Install

Install Matt's skills first, then this. House records the Matt version it has been reviewed against in `matt.json`.

**Claude Code**

```sh
claude plugin marketplace add mattpocock/skills
claude plugin install mattpocock-skills@mattpocock
claude plugin marketplace add KallendJack/house
claude plugin install house@kallendjack
```

**Codex**

```sh
codex plugin marketplace add mattpocock/skills
codex plugin add mattpocock-skills@mattpocock
codex plugin marketplace add KallendJack/house
codex plugin add house@kallendjack
```

Then, in a repo, ask the agent to "set up house".

## Working with House

Choose the work, then use Matt's skills directly. Start with `ask-matt` when unsure which fits.
House does not choose tasks or add an orchestration workflow.

Planned work and bugs live in GitHub Issues. Milestones group deliverable outcomes; native blocking links
express dependencies. Small incidental fixes can go straight into a PR. Each project keeps its own code layout,
checks and deployment rules, with shared agent documentation under `docs/agents/`.

The weekly Matt watch opens an issue when his version changes. Review the upstream changelog, remove House
rules now covered upstream, bump House's version, and roll the reviewed release into consuming repos through
separate PRs. Updating an installed plugin does not update a repo's copied conventions.

## Check

```sh
node --test configs/check-size.test.ts
```

## Licence

MIT
