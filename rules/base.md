## House rules

From the house repo (`KallendJack/house`, `rules/base.md`); change them there, not here. House version:
{{house}}, reviewed against Matt's skills {{matt}}.

- **Skills:** Matt Pocock's skills run the work (`grill-with-docs`, `to-spec`, `to-tickets`, `implement`,
  `code-review`, `pr`); when unsure which fits, `ask-matt` says. Where his skills have a rule, it wins; the house
  rules only fill the gaps.
- **Work** starts from an item where `docs/agents/issue-tracker.md` says work lives. Before building one, check its
  comments and open PRs for a claim, then comment "Building this".
- **Words** live in `GLOSSARY.md`; decisions that are hard to reverse or surprising are short ADRs in `docs/adr/`.
- **Branches** start from the default branch and rebase on it. A pull request that needs another waits for it to
  merge rather than carrying its branch.
- **Checks:** run the quick checks (lint, typecheck, unit tests, the specs you changed) before pushing; the full
  browser suite runs in CI. After pushing, watch CI and fix what fails before calling the work ready.
- **Merging** waits for green checks and a review against the issue. A pull request the owner will see says how to
  try it.
- **Prompts:** in a project with model evals, a change to what a model is told runs them 3 times on Claude and 3
  on Codex; each case passes at least 2 of 3 on each before it merges.
- **Docs** move with the change, in the same pull request, each kind in one place: `README.md` (what the repo is,
  how to run, check and deploy it, its features in a line each), `AGENTS.md` (how agents work here; `CLAUDE.md`
  only points to it), `GLOSSARY.md`, `docs/adr/` (decisions), `docs/agents/` (agent extras), `.env.example`.
- **Secrets** come from the environment, each listed in `.env.example`. Examples and fixtures are made up; the
  owner's and real people's data stays out of the repo.
- **Dependencies** stay few and locked, the platform's own pieces first. Vendored files say where they came from.
- **Dead code** and config are deleted.
- **Talking to the owner:** plain words and short; name things, not issue numbers; show work as screenshots with a
  one-line review and a short list of decisions, each with a recommendation. Technical calls are yours, made and
  noted; what they want, what it looks like and what to cut are theirs.
- **App code:** before writing or changing code, read `docs/agents/code.md`.
- **Screens:** before building or changing anything a person sees, read `docs/agents/screens.md`.
- **This repo's own rules** follow this section; they add to it and win where they say more.
