# house

The rules, configs and skills every one of my repos follows, whatever the project, on top of
[Matt Pocock's skills](https://github.com/mattpocock/skills).

- **Rules:** a short base for every repo's `AGENTS.md`, plus extras for app code and screens.
- **Configs:** strict TypeScript, Biome, and a size check (400 lines a file, 15 files a folder).
- **Skills:** `house-setup` writes the standard into a repo or brings it up to date; `lead` keeps a repo's ready work
  moving: pick, build, review against the issue and the agreed design, merge.

## Install

Install Matt's skills first, then this. Both update themselves.

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

## Check

```sh
node --test configs/check-size.test.ts
```

## Licence

MIT
