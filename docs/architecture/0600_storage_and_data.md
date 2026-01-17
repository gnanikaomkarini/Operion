# 0600: Storage and Data (Implementation Spec)

## File Layout

Operion adheres to the **XDG Base Directory Specification** on Linux.

| File Type | Default Path | Environment Variable |
| :--- | :--- | :--- |
| **Configuration** | `~/.config/operion/config.toml` | `$XDG_CONFIG_HOME` |
| **Activity Database** | `~/.local/share/operion/activity.db` | `$XDG_DATA_HOME` |
| **Logs** | `~/.local/state/operion/operion.log` | `$XDG_STATE_HOME` |

## Database Schema (SQLite)

Activity data is stored in a local SQLite database using the `rusqlite` crate. Timestamps are stored as UTC Unix integers (seconds).

### DDL

```sql
-- Tracks detailed focus changes (active window)
CREATE TABLE IF NOT EXISTS activity_log (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    timestamp INTEGER NOT NULL,          -- Unix epoch (seconds)
    app_id TEXT NOT NULL,                -- e.g., "org.gnome.TextEditor"
    window_title TEXT,                   -- Scrubbed title
    duration INTEGER NOT NULL,           -- Seconds active
    mode_id TEXT NOT NULL                -- The mode active at this time
);

-- Tracks system mode switches
CREATE TABLE IF NOT EXISTS mode_log (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    timestamp INTEGER NOT NULL,
    mode_id TEXT NOT NULL,
    trigger TEXT NOT NULL                -- "manual", "calendar", "auto"
);

-- Indices for performance
CREATE INDEX IF NOT EXISTS idx_activity_timestamp ON activity_log(timestamp);
CREATE INDEX IF NOT EXISTS idx_mode_log_timestamp ON mode_log(timestamp);
```

## Data Lifecycle



-   **Write Frequency:** Buffered writes occur every 30 seconds or on mode switch to minimize disk I/O.

-   **Concurrency:** **WAL (Write-Ahead Logging) Mode** is mandatory (`PRAGMA journal_mode=WAL;`) to allow simultaneous readers and writers. This ensures the Journal UI can write to the DB while the Daemon is reading/writing.

-   **Retention:** By default, data is retained for 90 days. A generic `VACUUM` and prune operation runs weekly.