# Implementation: Asking you apart from agent time

## Tasks

### T-01 — Asking you apart in the panel

Status: done

- `hooks/register.tsx`, the `Pane` hook: Asking you is taken out of the work-mix totals before the bars, percentages and the header's `agent` total are worked out, and drawn as a dimmed `Asking you` row, with its time and no bar or percentage, just above Waiting on you once it reaches a second. The band, its totals and the panel timeline's per-turn strips are untouched and keep Asking you.
- `tests/render.test.tsx`: two new tests, "the panel leaves a question out of the agent time and shows it beside Waiting on you; the band keeps it" and "the panel shows no Asking you row for a question answered in under a second, nor counts it", both on terminal and desktop. The palette tests in `expectColors` expected a totals bar for every category; Asking you now has none, so for it they check only its piece of the turn's strip.
- `README.md`: the panel section describes the Asking you row and that it isn't counted as working time.
- `docs/mockups.mjs`, `docs/panel.svg`: the panel image gains an `Asking you 1m12s` row above Waiting on you, which drops to 22m26s so the session still adds up. Ran `node docs/mockups.mjs`; only `panel.svg` changed. Screenshotted it with headless Chrome: rows aligned, nothing overlapping.
- Checks: `claude plugin validate .` passed (with the existing warnings), `claude plugin test .` 37 pass, 0 fail, `npx -p typescript tsc -p .` clean.

## Scenarios

- panel "Subagents worked longer than the session": tests/render.test.tsx "the panel puts two subagents on their own row beneath main-loop rows that add up to the session", passed
- panel "No subagents": tests/render.test.tsx "the panel draws no Subagents row when no subagent ran", passed
- panel "A question in the middle of a turn": tests/render.test.tsx "the panel leaves a question out of the agent time and shows it beside Waiting on you; the band keeps it", passed
- panel "A question shorter than a second": tests/render.test.tsx "the panel shows no Asking you row for a question answered in under a second, nor counts it", passed

## Reconciliation

- panel: applied to grove/specs/panel/spec.md
