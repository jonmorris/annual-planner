# Case study: Annual Planner

A running, modular case study of this project, written for a portfolio.
Repo-only: never built or shipped. Facts and dates come from
[DECISION-LOG.md](DECISION-LOG.md). This file turns them into a story.

## How this file works

- **Modules, not chapters.** Each `##` section stands alone, so a write-up can
  pick modules and drop the rest without leaving a gap.
- **Tag lines.** Every module opens with an italic tag line:
  - **Core**: the spine of any version.
  - **Optional**: for the long form, or for a specific audience named in
    brackets.
  - **Evidence**: what to show beside the text, marked `[ ]` until it has been
    captured and `[x]` after.
- **Running.** When work is worth telling, add or amend a module and add a row
  to *Log of additions*. Facts and dates come from DECISION-LOG.md. This file
  is where they become a story.
- **Placeholders** go in `[[double brackets]]` for the owner to fill in (role,
  tools, metrics, reflections). Never invent those.

## Suggested cuts

| Form | Modules |
|---|---|
| Short (one screen) | 1, 2, 4, 9 |
| Standard | 1, 2, 3, 4, 5, 6, 8, 9 |
| Long | 1–10 |

## 1. Overview

*Core · Evidence: [ ] screenshot of the Weekly view, [ ] screenshot of the Planning view, [ ] live link*

Annual Planner is a personal planning tool that runs in the browser. It lets you
set a goal for the year, for each of six two-month sprints, for each month and
for each week, and keeps a set of notes for every week. It is one HTML file. It
has no account and no server, and your plans stay in your own browser.

- **Role:** [[your role, e.g. sole designer and developer]]
- **Timeline:** first version committed 14 April 2026. [[how long it took to build; whether it has been in use since]]
- **Tools:** HTML, CSS and plain JavaScript, written with an AI coding assistant ([[name the tools and how you split the work]])
- **Live:** [[public URL, if deployed]]

## 2. The problem

*Core · Evidence: [ ] [[a before artefact: the notebook, spreadsheet or app this replaced]]*

[[What wasn't working before. The problem you, or the people you built it for,
had with planning a year. What the existing tools got wrong.]]

What the finished product shows the problem to be: long-range goals and this
week's work tend to drift apart. The planner keeps all four levels (year,
sprint, month, week) on screen together, so the week is always read against the
bigger plan.

## 3. Reframing the brief

*Core · Evidence: [ ] [[early sketch or notes, if any]]*

[[The brief as you first had it, e.g. "a yearly planner", and how it changed.]]

The finished design treats the year as six **two-month sprints**
(Jan–Feb, Mar–Apr and so on), not as quarters or a single list of goals. A
sprint is long enough for a meaningful goal and short enough to review often,
and it sits between the month and the year. [[Confirm this was the reasoning,
or replace it with yours.]]

## 4. One file, no build, no backend

*Core · Evidence: [ ] repo tree showing the single `index.html`, [ ] file size (about 36 KB)*

The whole app is one self-contained `index.html`, with inline styles and
scripts, no framework, no dependencies and no build step. Data is saved to the
browser's `localStorage`, under one versioned key per year
(`annual-planner-YYYY-v1`).

The trade-offs:

- **Gained:** nothing to install, update or host beyond a static file; it works
  offline once loaded; and nobody else holds your plans.
- **Given up:** plans don't sync between devices, and clearing browser data
  wipes them. **Export/Import** to a JSON file is the answer to both. Export
  deliberately covers every year's data, not only the current year's.

[[Why you chose this over a framework or a hosted backend: speed, privacy,
longevity, or something else.]]

## 5. Designing two views of the same plan

*Core · Evidence: [ ] Weekly view, [ ] Planning view, [ ] short clip of switching between them*

The same data is shown two ways:

- **Weekly view (default)** opens on the current week. It shows that week's
  goal with the month, sprint and year goals stacked beneath it, so the
  context is always one glance away. Arrow keys or a swipe move to the next or
  previous week.
- **Planning view** lists every week of the year, grouped under its sprint, with
  all four goals and the week's notes on each card. "View →" jumps back to that
  week in the Weekly view.

Each level has its own colour, used in both views: blue for the week, teal for
the month, amber for the sprint and purple for the year. Goals are edited in
place by clicking them. Esc cancels, and ⌘↵ or clicking away saves.

[[What you tried before landing on this, and any feedback that shaped it.]]

## 6. The calendar edge cases

*Optional [engineering audience] · Evidence: [ ] `generateWeeks()` excerpt from index.html*

Weeks run Sunday to Saturday, starting on the Sunday on or before 1 January,
so the year can have up to 54 weeks. A week that straddles two months belongs
to the month, and therefore the sprint, that it **starts** in. This rule keeps
every week in exactly one month and one sprint, at the cost of a week labelled
"January" ending in February. [[Whether you considered ISO weeks or Monday
starts, and why you didn't use them.]]

## 7. Saying no on the record

*Optional [product audience] · Evidence: [ ] [[link to Deferred rows in DECISION-LOG.md, once there are any]]*

What the planner leaves out, as of the first version:

- No accounts, sync or server.
- No tasks, checklists or due dates: one goal per level, plus notes.
- Only the current calendar year can be viewed. Other years' data is kept and
  exported, but can't be browsed.

None of these has a written reason yet. [[Which were deliberate choices and
why. Log each one as a Deferred decision before telling it here.]]

## 8. Quality

*Core · Evidence: [ ] [[phone and desktop screenshots]], [ ] [[any test or review notes]]*

The app escapes everything it renders that a user typed, works with touch and
keyboard, and its layout is set up for phone screens. It has no automated tests.
[[How you checked it: devices and browsers you tried, any bugs you found and
fixed.]]

## 9. Outcome and reflection

*Core · Evidence: [ ] [[usage data or a quote, if any]]*

[[What happened after launch: who uses it, how often, what changed for you.]]

[[What you'd do differently, and what you'd build next.]]

## 10. Working with an AI collaborator

*Optional [audiences interested in AI-assisted practice] · Evidence: [ ] CLAUDE.md, [ ] [[an example exchange or PR]]*

On 15 April 2026, the day after the first commit, the project adopted written
guidelines for its AI coding assistant (`CLAUDE.md`). They say to think before
coding, keep it simple, make surgical changes and verify against stated goals.
In November 2026 the project added this case study and a decision log, so the
reasoning behind changes is written down as they happen rather than rebuilt
from diffs afterwards.

[[How you split the work with the assistant, where it helped and where you
overrode it.]]

## Log of additions

| Date | Module | Change |
|---|---|---|
| 2026-11-19 | 1–10 | Initial draft from git history and the first-version code |
