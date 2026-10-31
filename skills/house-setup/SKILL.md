---
name: house-setup
description: House standard for a repo: write it into a new repo, or bring an existing repo's copy up to date. Use when the user says "set up house" or "house check", or when starting a new repo.
---

# House setup

The house repo holds the standard every repo follows: `rules/base.md` (the `## House rules` section of each repo's
`AGENTS.md`), `rules/code.md` and `rules/screens.md` (the extras), and `configs/` (TypeScript, Biome, the size check).
This skill writes them into a repo, or offers the changes when the repo's copy differs.

## Steps

1. **Find the house copy.** Read the files from this skill's plugin (its `rules/`, `configs/`, `matt.json` and
   `.claude-plugin/plugin.json`, two folders up from this file). If you can't, read them from
   `https://github.com/KallendJack/house`.
2. **Matt's setup.** Run `setup-matt-pocock-skills` if the repo has no `docs/agents/issue-tracker.md`, or if Matt's
   `CHANGELOG.md` says to re-run it in any version after the one the repo's House rules line names. Let it finish.
3. **The base.** In the repo's `AGENTS.md`, replace the `## House rules` section (up to the next `##` heading) with
   `rules/base.md`, or add it after the title, filling `{{house}}` with house's `version` and `{{matt}}` with
   `matt.json`'s `reviewed`. Keep everything else in `AGENTS.md`: the repo's own rules follow the section and win
   where they say more.
4. **The extras that apply.** Copy `rules/code.md` to `docs/agents/code.md` if the repo has app code, and
   `rules/screens.md` to `docs/agents/screens.md` if anything in it is seen by a person. A config-only repo takes the
   base alone; drop the base's pointer lines for extras it doesn't take.
5. **The configs, for a TypeScript repo:** copy `configs/tsconfig.house.json` and `configs/biome.house.json` to the
   root and extend them from the repo's own `tsconfig.json` and `biome.json`; copy `configs/check-size.ts` to
   `scripts/` and add `node scripts/check-size.ts` to the repo's check script. A repo with files already over runs it
   once with `--baseline`.
6. **The repo basics,** for every repo:
   - `configs/.gitattributes` to the root (LF line endings everywhere, so Windows and CI agree);
   - `CLAUDE.md` holding only "Read AGENTS.md.";
   - `.env.example` if the repo reads any environment variable;
   - for a TypeScript repo: the standard commands (`dev`, `check`, `e2e`, `build`) in `package.json`,
     `packageManager` and `engines` pinned, and `configs/github/ci.yml` and `configs/github/dependabot.yml` copied
     to `.github/workflows/ci.yml` and `.github/dependabot.yml`, adjusted to the commands the repo has;
   - a `LICENSE` if the repo is public (ask the user which).
7. **Open a pull request** with the `pr` skill and tell the user in a sentence or two what changed and why. Done
   when the pull request is open and its CI is green.
8. **Settings on GitHub,** after the pull request merges (ask before changing any): protect the default branch so
   it takes only green pull requests, and turn on secret scanning with push protection
   (`gh api -X PATCH repos/<owner>/<repo> -f security_and_analysis[secret_scanning][status]=enabled` and the same for
   `secret_scanning_push_protection`).

## Rules

- Change only what the house owns. A repo's own rules are the owner's.
- A house rule that's wrong for one repo is overridden in the repo's own section; the copied block stays as house wrote it.
- A rule worth having everywhere goes in the house repo first, in its own pull request, then out to the repos.
