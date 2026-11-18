## House rules

From `KallendJack/house`, `rules/base.md`. House version: {{house}}, reviewed against Matt's skills {{matt}}.
Change shared rules in House; keep project-specific rules below this section.

- **Workflow:** work follows Matt Pocock's main flow; `ask-matt` has the map. Build each ticket with his
  `implement` skill, which drives `tdd` and ends with `code-review`; asked to build one without `/implement`,
  read that skill's `SKILL.md` and follow its steps anyway. Write PR bodies with his `pr` skill. His rules take
  precedence over House. The owner chooses the work.
- **Work tracking:** planned work and bugs live where `docs/agents/issue-tracker.md` says. Small incidental fixes
  can go straight into a PR. Milestones group deliverable outcomes; blocking links express dependencies.
- **Checks:** run the repo's checks before pushing. Fix failing CI before calling a PR ready; merge requires
  green checks and review against the requested change.
- **Docs:** `README.md` explains the project; `AGENTS.md` holds agent instructions; `CLAUDE.md` points to it.
  A folder whose purpose isn't obvious gets a short README, linked from its parent; link to detail, don't repeat it.
  Matt's setup owns the tracker and domain-document pointers in `docs/agents/`. Update docs, folder READMEs and
  their links with the change; CI checks local Markdown links and anchors.
- **Secrets:** values come from the environment, names from `.env.example`. Public examples and fixtures use
  made-up data.
- **Communication:** plain words, concise explanations, and evidence appropriate to the change.
- **App code:** before writing or changing code, read `docs/agents/code.md`.
- **Screens:** before building or changing screens, read `docs/agents/screens.md`.
- **Project rules** below add to these conventions and override House where explicitly stated.
