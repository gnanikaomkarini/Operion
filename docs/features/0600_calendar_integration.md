# 700: Calendar Integration

## iCal Parsing

Operion parses standard `.ics` files to schedule mode locks. It supports both local files and remote URLs (Google Calendar, Outlook, etc.).

-   **Library:** `ical` crate.
-   **Sources:**
    -   **Local File:** Watched for changes via filesystem events.
    -   **Remote URL:** Fetched via HTTP/HTTPS on a configurable polling interval (default: 15 minutes).
-   **Sync:** Updates internal schedule cache upon file change or successful poll.

## Mode Mapping

Events are mapped to modes via regex in the event summary.
-   `"Meeting [work]"` -> Locks `work` mode.
-   `"Lunch [chill]"` -> Locks `chill` mode.

## Locking Mechanism

When a calendar event starts:
1.  Controller sets `system_state.locked_until = event_end_time`.
2.  Manual mode switch attempts are rejected with `Error::ModeLocked`.