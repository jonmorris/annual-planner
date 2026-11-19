# Decision log

A dated, one-line-per-decision index of what this project decided. It is a
pointer, not a second source of truth. Each row's **Ref** names the file and
section where the reasoning lives:

- [`DECISIONS.md`](DECISIONS.md) holds the reasoning for decisions that have no
  other home.
- [`../CLAUDE.md`](../CLAUDE.md) holds working conventions.
- [`../index.html`](../index.html) section banners (`CONSTANTS`, `WEEK GENERATION`,
  `PERSISTENCE`, `RENDER`, `EDITING`, `KEYBOARD & SWIPE`) show where a decision
  is implemented, but not why it was made.
- **git history** means the decision is visible in a commit, but its reasoning
  was never written down.

Repo-only: this file is never built or shipped.

## How to keep this file

- **Add a file, not a row.** A new decision goes in
  [`decision-log/`](decision-log/) as its own file named
  `YYYY-MM-DD-short-name.md` (lowercase, hyphenated), holding exactly one table
  row. Never edit the table on a branch: rows appended to the same last line by
  parallel branches always conflict, and separate files never do.
- **Fold on main.** Append the waiting entries to the end of the table in
  filename order (date, then name) and delete their files. Run it on `main`,
  in a commit of its own, whenever the folder gets long. The `## Log` table
  must stay the last thing in this file.

      for f in docs/decision-log/2*.md; do cat "$f" >> docs/DECISION-LOG.md && git rm -q "$f"; done
      git commit -m "Fold decision-log entries"

- **One row per decision, not per commit.** A reversed decision gets a new row
  of kind Reversed. The old row stays.
- **Say the decision, not the change** ("Export covers every year's data", not
  "edit exportData").
- **Kind** is one of the following. This is the only place the list is kept:

  | Kind | Use for |
  |---|---|
  | Product | What the planner does and for whom: features, scope, data it keeps |
  | Design | How it looks and behaves: layout, views, colour, interaction |
  | Engineering | How it's built and hosted: structure, storage, dependencies |
  | Process | How work on the repo is done: conventions, records, review |
  | Deferred | Something considered and deliberately not done (yet) |
  | Reversed | A new row that undoes an earlier one; name the old row's date |

- **Ref** names the file → section holding the why. If no why is written
  anywhere, write it there first (in `DECISIONS.md` if there's no better home).
- **Entry format.** One non-blank line, starting and ending with `|`, with
  exactly four cells. The Date cell matches the filename date, Kind is from the
  list above, and Decision and Ref are non-empty. There is no toolchain to
  enforce this, so check by eye before folding. This lists any badly named
  files:

      ls docs/decision-log | grep -vE '^(README\.md|[0-9]{4}-[0-9]{2}-[0-9]{2}-[a-z0-9]+(-[a-z0-9]+)*\.md)$'

## Log

| Date | Kind | Decision | Ref |
|---|---|---|---|
| 2026-04-14 | Engineering | The whole app is one self-contained `index.html` (inline CSS and JS, no framework, no build step, no dependencies) | git history (b25df75) |
| 2026-04-14 | Product | Plans nest year → six two-month sprints → month → week, with a free-form notes field per week | git history (b25df75); index.html → CONSTANTS, STATE |
| 2026-04-14 | Engineering | Weeks run Sunday to Saturday, and each week belongs to the month and sprint it starts in | git history (b25df75); index.html → WEEK GENERATION |
| 2026-04-14 | Engineering | Data stays in the browser's localStorage, one versioned key per year, with no backend or accounts | git history (b25df75); index.html → PERSISTENCE |
| 2026-04-14 | Product | JSON export and import, covering every year's data, are the way to back up or move plans | git history (b25df75); index.html → PERSISTENCE |
| 2026-04-14 | Design | Two views: a Weekly focus view that opens on the current week, and a Planning view listing every week grouped by sprint | git history (b25df75); index.html → RENDER |
| 2026-04-14 | Design | Each level has its own colour: blue week, teal month, amber sprint, purple year | git history (b25df75); index.html → `:root` styles |
| 2026-04-14 | Design | Goals are edited in place by clicking them; Esc cancels and ⌘↵ or blur saves | git history (b25df75); index.html → EDITING |
| 2026-04-14 | Design | Arrow keys and swipe move between weeks in the Weekly view | git history (b25df75); index.html → KEYBOARD & SWIPE |
| 2026-04-15 | Process | AI-assisted changes follow written guidelines: think first, keep it simple, make surgical changes, verify against goals | CLAUDE.md |
