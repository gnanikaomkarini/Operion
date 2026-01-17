# 0200: Operion Controller (Daemon)

## Architecture

The Controller (`operiond`) is the primary executable. It implements an event-driven architecture using the `tokio` runtime.

## Event Loop

The main loop processes events from multiple asynchronous channels:

1.  **System Events:** Window focus changes, idle timers.
2.  **User Commands:** D-Bus method calls (e.g., `SetMode`).
3.  **File Watchers:** `notify` events on configuration/calendar files.
4.  **Tickers:** Periodic tasks (e.g., every 60s check for calendar events).

## State Machine

The system state is protected by a `RwLock`.

```rust
struct SystemState {
    active_mode: ModeId,
    locked_until: Option<DateTime<Utc>>,
    active_window: Option<WindowInfo>,
    is_idle: bool,
}
```

## Mode Transition Logic

When a transition is requested:
1.  **Validation:** Check if current mode is locked (time-based).
2.  **Teardown:** Revert changes from previous mode (e.g., kill launched processes).
3.  **Setup:** Apply new mode settings (theme, wallpaper, app blocking).
4.  **Persistence:** Log the transition to `mode_log` table.