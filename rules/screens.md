# Screens

Read before building or changing anything a person sees.

## Design: what's signed off is what's built

- **Paper first.** Each screen is built from a board the owner agreed in the repo's Paper file, linked from its
  issue. The file has four pages: `1 · Live` (screenshots of the built app only), `2 · Agreed` (OK'd, not yet built
  as drawn), `3 · Drafts`, `4 · Archive`. New work starts on Drafts, from a screenshot of the built screen where one
  exists.
- **An issue that changes what the owner sees** links its agreed board before it's ready to build, and covers the
  whole board or says which parts it leaves out and where they're covered. A change with nothing new to see names the
  board that already covers it.
- **The pull request puts screenshots beside each board it builds**, at every size the board is drawn for, and lists
  every difference. An unlisted difference doesn't merge; a listed one needs the owner's OK. "Close enough, with a
  follow-up" is not a merge. A review checks the screenshots against the board, not only the code against the issue.
- **On merge,** a board built as drawn moves from Agreed to Archive, and the new screenshot goes on Live. Otherwise
  the board stays in Agreed and the gap is written on its issue.
- **Labels say what's happening,** never what isn't: "in the green", not "no tape".

## Look

- **One theme of tokens.** Colours, type sizes, spacing and radii are tokens named by meaning (brand, danger, muted),
  and every style uses them by name. One global stylesheet holds the base styles; the rest is styled through the
  project's styling system, picked with its stack.
- **Shared pieces.** Buttons, inputs, fields and error lines come from `components/`; when one doesn't fit, give it
  an option rather than a hand-styled copy.
- **With Tailwind:** the tokens live in `@theme`; shared components may start from shadcn/ui, copied in and themed
  with the tokens.

## Behaviour

- A screen shows what the user needs now and what they must act on (errors, flagged items); the rest is one tap
  away. Calm: no nags, no warnings nobody asked for.
- Zero layout shift: what loads later holds its final size from the first frame.
- Content that loads after the page fills skeleton rows, and a revisit shows the last answer at once. A button
  shows when it's busy.
- Forms keep what was typed on an error and show the error beside its field.
- **Errors and warnings say what to do,** in plain words: what happened and the next step ("Couldn't save, you're
  offline. It'll retry when you're back."), never a code or a bare "Something went wrong".
- **Empty screens point the way:** what goes here and the one action that fills it.

## Access

- WCAG 2.2 AA: contrast, a visible focus ring, labels, real buttons and links. Every screen works at 390 wide and
  by keyboard.
- Each Playwright spec runs axe (`@axe-core/playwright`) on the pages it visits.
