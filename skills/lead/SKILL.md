---
name: lead
description: Lead a repo's ready work through to merged, round by round, on top of Matt Pocock's skills. Use when the user says "lead", "keep building" or "what's next", or wants work kept moving while they're away.
---

# Lead

Keeps a repo's ready work moving. Matt's skills build and review; the lead adds the order, the board check, the
evals and the merge. Work in **rounds**: one item per round, from pick to merged.

## Each round

1. **Main first.** A red default branch is the round's item, ahead of everything.
2. **Pick** the first issue the repo's triage labels mark ready to build, in milestone order, that's unclaimed (no
   "Building this" comment in the last 12 hours, no open PR), unblocked, and touches different files from any item
   in progress.
3. **Claim** it with a "Building this: <who> (<branch>)" comment. Stopping without a PR, comment "Stopped: <why>".
4. **Build** with `implement` (or `implement-spec` for a whole spec) on a branch from the default branch, in its own
   worktree, until the quick checks pass locally.
5. **Open the PR** with the `pr` skill, with screenshots beside each board it builds and every difference listed
   when the owner will see the change (`docs/agents/screens.md`).
6. **Review** in a fresh session: `code-review` against the issue, the screenshots against the board, and the evals
   when the House rules' Prompts line applies. The builder fixes each finding or answers it with a reason. After 3
   rounds of review that don't pass, hand it to the owner with the findings and both sides.
7. **Merge** with a merge commit once every check is green, the review passed and each board difference has the
   owner's OK; then move the boards as `docs/agents/screens.md` says. The round is done when the item is merged or
   handed to the owner.

## CI

- A check failing in a test the PR didn't touch is re-run once; a second failure is real.
- A branch behind the default branch that fails is brought up to date first.
- Push fast-forward only: to branches you started, or to an open PR's branch once you've checked it's still open.

## The owner

One batched message per round at most: what needs their OK (each with a recommendation), what to try, what's
stuck.
