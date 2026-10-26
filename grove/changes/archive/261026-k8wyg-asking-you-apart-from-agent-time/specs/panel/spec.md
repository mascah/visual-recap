# Changes to panel

The changes that change 261026-k8wyg proposes to the requirements of `panel`, the Recap pane opened with `/visual-recap`. This is future work. It starts from the maintained spec [grove/specs/panel/spec.md](../../../../specs/panel/spec.md) at `649dec8`.

## MODIFIED Requirements

### Requirement: Work-mix totals with a Subagents row

The system shall draw the panel's totals as the work-mix totals in `time-accounting`: one row per main-loop category other than Asking you, adding up to the session's main-loop active time less Asking you, then a separate Subagents row beneath them.

#### Scenario: Subagents worked longer than the session

- GIVEN a 5-minute session in which the main loop ran Shell throughout and two subagents each ran for the whole 5 minutes
- WHEN the panel draws
- THEN the main-loop rows show Shell 5m, and a separate Subagents row beneath them shows 10m

#### Scenario: No subagents

- GIVEN a session in which no subagent ran
- WHEN the panel draws
- THEN no Subagents row is drawn

## ADDED Requirements

### Requirement: Asking you apart from agent time

Where the main loop spent at least a second asking you, the system shall leave that time out of the panel's `agent` total and its percentages, and draw it as a dimmed Asking you row with its time and no bar or percentage, above the Waiting on you row.

#### Scenario: A question in the middle of a turn

- GIVEN a turn in which the main loop thinks for 30 seconds, asks you a question that waits 60 seconds, then runs Shell for 30 seconds
- WHEN the panel draws
- THEN the header shows `agent 1m00s`, the bars show Thinking and Shell at 50% each, and a dimmed Asking you row shows 1m00s with no bar or percentage

#### Scenario: A question shorter than a second

- GIVEN a turn in which the main loop asked you a question answered in under a second
- WHEN the panel draws
- THEN no Asking you row is drawn, and that time is in neither the bars nor the `agent` total
