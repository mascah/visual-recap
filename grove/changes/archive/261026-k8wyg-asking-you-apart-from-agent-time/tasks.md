## T-01 — Asking you apart in the panel

Result: the panel follows [specs/panel/spec.md](specs/panel/spec.md), and the README and its panel image say so.

Files: `hooks/register.tsx`, `tests/render.test.tsx`, `README.md`, `docs/mockups.mjs`, `docs/panel.svg`

Constraints: the band, its totals and the panel timeline's per-turn strips keep Asking you; `time-accounting`'s totals are unchanged.

Acceptance:
- A render test drives "A question in the middle of a turn" and finds the header's `agent 1m00s`, Thinking and Shell at 50%, and the dimmed Asking you row, on terminal and desktop.
- The same session's band still shows Asking you in its strip and totals.
- A render test drives "A question shorter than a second" and finds no Asking you row.
- The existing Subagents-row tests still pass.
- README's panel section describes the Asking you row; `docs/panel.svg` is redrawn with one and checked in a browser.
- `claude plugin validate .`, `claude plugin test .` and `npx -p typescript tsc -p .` pass.
