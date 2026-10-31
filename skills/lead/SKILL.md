---
name: lead
description: Run a milestone's work through to merged, the house way, on top of Matt Pocock's skills. Use when the user says "lead", "keep building", "what's next", or asks to keep a repo's work moving while they're away.
---

# Lead

Keeps a repo's ready work moving: picks the next item, builds it with Matt's skills, reviews it against its issue and
board, and merges it when it's green and matches. Matt's skills do the building and reviewing; this adds the order,
the board check, the evals and the merge.

## Each round

1. **Main first.** If the default branch's CI is red, fixing it is the next item, ahead of everything.
2. **Pick the next item:** the first issue marked ready to build (the repo's triage label for it), in milestone
   order, that nobody has claimed (no "Building this" comment in the last 12 hours, no open PR), isn't blocked by an
   open issue, and doesn't touch the same files as one being built.
3. **Claim it:** comment "Building this: <who> (<branch>)". Stopping without a PR, comment "Stopped: <why>".
4. **Build** with `implement` (or `implement-spec` for a whole spec), on a branch from the default branch, in its own
   worktree. Quick checks locally; the full browser suite runs in CI.
5. **Open the PR** with the `pr` skill. If the owner will see the change, it carries screenshots beside each board it
   builds and lists every difference (`docs/agents/screens.md`).
6. **Review** with a fresh session: `code-review` against the issue, plus the screenshots against the board. If the
   change alters what a model is told, run the project's evals 3 times on Claude and 3 on Codex. The builder fixes
   each finding or answers it with a reason; after 3 rounds that don't pass, it goes to the owner with the findings
   and both sides.
7. **Merge** with a merge commit when every check is green, the review passed, and any board difference has the
   owner's OK. Move the boards on Paper as `docs/agents/screens.md` says. Then the next round.

## CI

- A check failing in a test the PR didn't touch is re-run once; a second failure is real.
- A branch behind the default branch that fails is brought up to date first.
- Never force-push, and never push to a branch you didn't start without checking it's still open and fast-forward.

## What goes to the owner

One message, batched: what needs their OK (board differences, decisions with a recommendation each), what to try,
and what's stuck. Nothing they don't need to act on.
