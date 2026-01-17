# 700: Calendar Integration

## iCal Parsing

Operion parses standard `.ics` files to schedule mode locks.

-   **Library:** `ical` crate.
-   **Sync:** File watcher triggers re-parse on modification.

## Mode Mapping

Events are mapped to modes via regex in the event summary.
-   `"Meeting [work]"` -> Locks `work` mode.
-   `"Lunch [chill]"` -> Locks `chill` mode.

## Locking Mechanism

When a calendar event starts:
1.  Controller sets `system_state.locked_until = event_end_time`.
2.  Manual mode switch attempts are rejected with `Error::ModeLocked`.