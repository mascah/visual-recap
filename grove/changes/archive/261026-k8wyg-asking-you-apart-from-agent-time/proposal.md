# Asking you apart from agent time

## Problem

Issue #9 (opened 2026-10-19): "Time spent in AskUserQuestion or ExitPlanMode is the agent waiting on the person, but it's counted with the agent's work."

What the code does at `649dec8` (`main`):

- The panel's header shows `agent` as the sum of the main loop's work-mix totals, Asking you among them (`hooks/register.tsx`, the `Pane` hook: `active` is the sum of `mix.main`, drawn as `agent {fmt(active)}`). The issue's own line reference, `hooks/register.tsx:233`, predates change 261020-0z6h5.
- Asking you is one of the panel's bars, and every bar's percentage is a share of that same `active` total, so a long question shrinks every other share.
- Time between turns is already set apart: the panel draws it as a dimmed "Waiting on you" row with no bar or percentage, once it reaches a second.

## Intended outcome

- The panel's `agent` total is time the main loop spent working, without time spent asking you.
- The panel's bars and percentages are shares of that time.
- Time spent asking you still shows in the panel, as its own dimmed row beside Waiting on you.
- The band is unchanged: its strips and totals keep Asking you.

## Scope

### In scope

- The panel's header total, bars and percentages, and a new Asking you row.
- README's panel section and the panel image drawn by `docs/mockups.mjs`.

### Out of scope

- The band: its wall-clock and work-mix strips and totals keep Asking you (see Decisions).
- The panel timeline's per-turn strips, which keep Asking you.
- How time is counted (`time-accounting`). Its categories and totals stay as they are; only how the panel presents them changes.
- Counting permission prompts as Asking you. That stays an open question in the maintained `time-accounting` spec (issue #10).

## Decisions

All of these were offered as recommendations and accepted by the owner with "yes".

- **The panel sets Asking you apart.** Asking you leaves the bars, the percentages and the header's `agent` total, and is drawn as a dimmed `Asking you` row with its time, just above "Waiting on you", once it reaches a second. Reason: it is the agent waiting on the person, like Waiting on you, which the panel already shows apart.
- **The band keeps Asking you.** The wall-clock strip, the work-mix strip and the band's totals are unchanged. Reason: asking happens inside a turn, and the band answers what the time is going to right now, which includes what is blocking.
- **The panel timeline's per-turn strips keep Asking you**, for the same reason as the band.
- **Only the panel spec changes.** Its work-mix requirement is modified to leave Asking you out of the rows, and a requirement for the Asking you row is added; `time-accounting` is untouched.
- **Routine defaults:** one task, in `hooks/register.tsx`, with a render test in `tests/render.test.tsx` on terminal and desktop, the README's panel section, and an Asking you row in the panel image from `docs/mockups.mjs`, with the images redrawn.

## Open questions

None.

## Related documents

- Requirements: [specs/panel/spec.md](specs/panel/spec.md)
- Tasks: [tasks.md](tasks.md)
- Issue #9, "Should \"Asking you\" count as agent time?"
