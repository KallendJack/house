# App code

Read before writing or changing code. Each rule is a concept any stack can follow; the "In TypeScript" lines say
how a TypeScript project does it, and a project on another stack does the same with its own tools. The house
configs enforce what a check can (`tsconfig.house.json`, `biome.house.json`, the size check).

## Stack

- **The project decides its stack,** tailored to what it is, with the owner when it starts, and records the choice
  and why in an ADR. From then on that ADR is the stack; changing it takes another.
- **Well-known tools, one per job:** one formatter and linter, one test runner, one way to validate data. The
  formatter decides formatting.
- **The house has configs for** TypeScript with pnpm, Biome, Vitest, Playwright and Zod. A project that picks them
  gets those configs; one that picks otherwise sets up the same checks with its own tools.

## Commands and CI

- **The same commands in every repo,** so anyone (or any agent) moving between repos knows them: `dev` (run it
  locally), `check` (lint, typecheck, size check, unit tests: the quick checks), `e2e` (browser tests), `build`.
  A repo without one of them leaves it out rather than renaming it.
- **Pinned versions:** the runtime and the package manager (`packageManager` and `engines` in `package.json`), and
  a lockfile, so a fresh clone runs the same as yours.
- **CI on every pull request** runs `check`, then `e2e` and `build`; the default branch is protected and takes
  only green pull requests.
- **Dependency updates** come grouped, weekly, through the same CI, and merge only when green.

## Structure

- **The default layout,** which a project adjusts in its own `AGENTS.md` (a `## Layout` section saying only what
  differs) or, for a bigger change, an ADR:

  ```text
  src/
  ├── features/<feature>/   one folder per feature: its pages or routes, logic, its own components; index.ts is its door
  ├── components/<kind>/    UI shared by two or more features, grouped by kind: buttons/, forms/, layout/, feedback/
  ├── lib/<topic>/          shared helpers, grouped by topic once there's more than a few
  └── main.ts               the entry: wires the features together
  e2e/                      browser tests; unit tests sit beside the file they test (x.test.ts)
  ```

- **No flat piles.** A folder holds one kind of thing. Past 15 source files it splits into subfolders by kind or
  topic, never into "misc" or "utils2"; the size check fails a folder that doesn't.
- **Names:** files in kebab-case, named after what they export; one component per file.
- **Vertical slices.** Each feature is one folder: its routes or pages, its logic, its browser code. A feature has
  one name everywhere: folder, routes, tests, glossary. Folders a framework fixes (`pages/`, `routes/`) stay thin
  and call into the feature's folder; otherwise follow the framework's own conventions.
- **One door per feature.** A feature's `index.ts` exports what others may use, kept small; other features import
  from it, never from its insides. A deep feature with a small door is easier to change and to hand to an agent.
- **A feature README only when it earns it:** when what the folder does or how it's used isn't plain from its door.
  The repo's `README.md` lists the features in a line each.
- **Shared code** sits in one place for UI pieces and one for helpers (`components/`, `lib/`); look there before
  writing one. Share knowledge, not look-alikes: code that must change together becomes one; code that merely looks
  alike stays apart until a third copy appears. UI pieces are shared at their second use, so the look stays
  consistent.
- **The entry file is the composition root:** it wires the features together and holds no logic.
- **Small files.** Source files stay under 400 lines (tests, fixtures and generated files aside); split by kind as
  they grow. The size check is a ratchet: files and folders already over are listed at their size, which may shrink
  and never grow.
- **One language per file.** Styles in stylesheets or classes, browser code in typed modules the build bundles,
  markup in components or templates, SQL in parameterised queries and migration files. Browser code imports the
  modules it shares with the server.
- **Single source of truth.** What's shown, counted or due is decided in one module, and everything that needs it
  imports it.

## Type safety

- **The compiler checks everything it can, at its strictest,** and nothing silences it: a wrong type is fixed, or
  the value is parsed.
- **Parse at every edge.** Data from outside (request bodies and forms, database rows, files, environment, every
  third-party or model response) is parsed into a typed value before anything uses it, and the type comes from the
  schema.
- **Make wrong states unrepresentable.** Each variant is its own case the compiler checks; expected failures are
  values the caller has to handle, and exceptions are for bugs.
- **In TypeScript:** `tsconfig.house.json`'s flags; `as const` and `satisfies` are the only casts, and Biome rejects
  `any` and `!`; Zod at the edges; discriminated unions, no enums; `type` over `interface`; `Result` at module
  boundaries; an options object past two parameters.

## Errors and security

- Every error is handled where it can be, or reaches the app's one error handler, which logs it with its context.
- Every route that reads or changes data checks who is asking. Forms that change data are protected from
  cross-site posts. Output goes through the framework's escaping; raw HTML is only ever the app's own.
- A schema change is a new migration; applied migrations stay as they are.

## Tests

- Test behaviour through what callers touch: HTTP, the page in a browser, a module's exported functions.
- Use real databases, files and git. Fake only what's outside the app's control (third-party APIs, email, the
  clock), passed in as dependencies.
- A bug gets a failing test first.
- Comments say why.
