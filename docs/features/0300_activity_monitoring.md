# 400: Activity Monitoring

## Data Collection

The `ActivityMonitor` module is responsible for capturing context.

## Active Window Tracking

-   **Mechanism:** Polls the GNOME Shell Extension via D-Bus every 1 second.
-   **Debouncing:** Writes to the database are debounced (30s buffer) to reduce I/O.
-   **Idle Detection:** Uses `org.gnome.Mutter.IdleMonitor` D-Bus interface.

## Data Structure

Collected events are transformed into `ActivityRecord` structs before storage.

```rust
struct ActivityRecord {
    timestamp: i64,
    app_id: String,
    window_title: String,
    duration: u32,
    mode: String,
}
```

## Privacy Controls

-   **Sanitization:** Window titles can be scrubbed via regex rules defined in config (e.g., removing email addresses).
-   **Local Only:** Hard constraint: No network telemetry.