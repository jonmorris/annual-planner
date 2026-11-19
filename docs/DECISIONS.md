# Decisions

Where the reasoning behind a decision lives when nothing else in the repo holds
it. Each `##` section is one decision: what was decided, why, and what it rules
out. [DECISION-LOG.md](DECISION-LOG.md) points here by section name.

Decisions made before this file existed (the initial build, April 2026) are
recorded in the log with **git history** as their Ref, because their reasoning
was never written down. If you write one up later, add a section here and a
new decision-log entry that points to it.

## Running decision log and case study

**Decided:** 2026-11-19. Keep a dated, one-row-per-decision index
(`docs/DECISION-LOG.md`) and a modular portfolio case study
(`docs/CASE-STUDY.md`). Both are repo-only and never shipped.

**Why:** Until now the reasoning behind this project has lived only in commit
diffs, which say what changed but not why. A short index that points at the
reasoning makes the history reviewable, and gives the case study facts and
dates to draw on instead of memory.

**How:** New decisions arrive as one-row files in `docs/decision-log/` and are
folded into the table on `main`, never edited into the table on a branch.
Parallel branches that each append a row to the last line of the same table
always conflict. Separate files never do.

**Rules out:** Adding a build step, test runner or package manifest just for
this. The repo has no toolchain, so validating and folding entries are shell
one-liners, documented in `DECISION-LOG.md`.
