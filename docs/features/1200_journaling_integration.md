# 1200: Journaling

## Session Review UI

This feature launches a transient GTK dialog upon mode exit.

## Trigger Logic

-   **Event:** `ModeChanged` (from `Work` -> `Any`).
-   **Condition:** Duration of `Work` session > 15 minutes.

## Implementation

-   **UI:** Spawns a dedicated GTK4 window (not part of the daemon, a separate child process).
-   **Storage:** Saves text input to a separate `journal_entries` table in SQLite, linked to the `mode_log` ID.

```sql
CREATE TABLE journal_entries (
    id INTEGER PRIMARY KEY,
    mode_log_id INTEGER,
    content TEXT,
    rating INTEGER,
    FOREIGN KEY(mode_log_id) REFERENCES mode_log(id)
);
```