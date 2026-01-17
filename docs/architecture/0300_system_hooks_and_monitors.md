# 0300: System Hooks & Monitors (Implementation Spec)

## Overview

The System Hooks & Monitors layer abstracts OS-specific interactions. For the initial MVP targeting **Zorin OS (GNOME/Wayland)**, this layer interacts with the desktop environment via D-Bus and direct system calls.

## Interface Definition

The `SystemMonitor` trait defines the contract for all platform implementations.

```rust
#[async_trait]
pub trait SystemMonitor {
    /// Returns metadata about the currently focused window.
    async fn get_active_window(&self) -> Result<WindowInfo>;

    /// Terminates the specified process.
    async fn kill_process(&self, pid: u32) -> Result<()>;

    /// Sets the global GTK theme using GSettings.
    async fn set_theme(&self, theme: &str) -> Result<()>;

    /// Sets the desktop wallpaper.
    async fn set_wallpaper(&self, uri: &str) -> Result<()>;
}
```

## GNOME Implementation (`GnomeSystemMonitor`)

### 1. Active Window Monitoring (Wayland)
On Wayland, external applications cannot directly query the active window title for security reasons. Operion relies on a companion **GNOME Shell Extension** to expose this data via D-Bus.

- **Bus:** Session Bus
- **Interface:** `org.gnome.Shell.Extensions.Operion`
- **Object Path:** `/org/gnome/Shell/Extensions/Operion`
- **Method:** `GetActiveWindowInfo() -> (s, s)` (Returns `app_id`, `title`)

### 2. Application Control
- **Discovery:** Iterates `/proc` to map application names to PIDs.
- **Enforcement:** Sends `SIGTERM` to processes violating the current mode's blacklist.

### 3. UI & Theme Control
Uses standard GLib/GSettings schemas.

- **Theme:**
  - **Schema:** `org.gnome.desktop.interface`
  - **Key:** `gtk-theme`
  - **Type:** `string`
  
- **Wallpaper:**
  - **Schema:** `org.gnome.desktop.background`
  - **Key:** `picture-uri` (and `picture-uri-dark`)
  - **Type:** `string` (URI format, e.g., `file:///...`)

## Error Handling
- **D-Bus Timeouts:** The monitor implements a 200ms timeout for window queries to prevent blocking the main loop.
- **Missing Extension:** If the GNOME Shell extension is unreachable, the system falls back to a "Degraded Mode" (logging warnings but continuing execution).