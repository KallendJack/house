## House rules

From `KallendJack/house`, `rules/base.md`. House version: {{house}}, reviewed against Matt's skills {{matt}}.
Change shared rules in House; keep project-specific rules below this section.

- **Workflow:** use Matt Pocock's skills directly; `ask-matt` routes when unsure. His rules take precedence over
  House. The owner chooses the work.
- **Work tracking:** planned work and bugs live where `docs/agents/issue-tracker.md` says. Small incidental fixes
  can go straight into a PR. Milestones group deliverable outcomes; blocking links express dependencies.
- **Checks:** run the repo's checks before pushing. Fix failing CI before calling a PR ready; merge requires
  green checks and review against the requested change.
- **Docs:** `README.md` explains the project; `AGENTS.md` holds agent instructions; `CLAUDE.md` points to it.
  Matt's setup owns the tracker and domain-document pointers in `docs/agents/`. Update docs with the change.
- **Secrets:** values come from the environment, names from `.env.example`. Public examples and fixtures use
  made-up data.
- **Communication:** plain words, concise explanations, and evidence appropriate to the change.
- **App code:** before writing or changing code, read `docs/agents/code.md`.
- **Screens:** before building or changing screens, read `docs/agents/screens.md`.
- **Project rules** below add to these conventions and override House where explicitly stated.
