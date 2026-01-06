# 0300: System Hooks & Monitors

## The Bridge to the Operating System

The **System Hooks & Monitors** are the components that interact directly with the underlying operating system. They are the "hands and eyes" of Operion, responsible for gathering information about the system and executing the commands issued by the **Operion Controller**.

This layer is inherently OS-specific. The way you get the active window title on Linux is different from how you do it on Windows or macOS. Therefore, this entire component is designed as a **pluggable interface**.

## The Interface-Driven Design

The Controller does not talk to any specific OS-level API. Instead, it talks to a generic `SystemMonitor` interface.

This interface defines a set of methods that every platform-specific implementation must provide.

### `SystemMonitor` Trait (Conceptual):

```rust
use std::path::PathBuf;
use async_trait::async_trait;

pub struct WindowInfo {
    pub app_name: String,
    pub window_title: String,
}

#[async_trait]
pub trait SystemMonitor {
    /// Returns info about the foreground window.
    async fn get_active_window_info(&self) -> Result<WindowInfo, anyhow::Error>;

    /// Returns a list of running application names.
    async fn get_running_apps(&self) -> Result<Vec<String>, anyhow::Error>;

    /// Blocks or hides an application.
    async fn block_app(&self, app_name: &str) -> Result<(), anyhow::Error>;

    /// Sets the system-wide GTK theme.
    async fn set_gtk_theme(&self, theme_name: &str) -> Result<(), anyhow::Error>;

    /// Sets the desktop wallpaper.
    async fn set_wallpaper(&self, file_path: &PathBuf) -> Result<(), anyhow::Error>;

    /// Begins monitoring the system for events and sends them to the Controller via a channel.
    fn start_monitoring(&self, sender: tokio::sync::mpsc::Sender<SystemEvent>) -> Result<(), anyhow::Error>;
}
```

## Pluggable Implementations

For the initial target platform, **Zorin OS (GNOME)**, we will create a concrete implementation of this trait.

-   `GnomeSystemMonitor`: This implementation will be highly specific to the GNOME desktop environment.
    -   To get window information, it will subscribe to focus change events on the D-Bus bus.
    -   To change themes and wallpapers, it will execute `gsettings` commands.
    -   To get a list of running applications, it may inspect the `/proc` filesystem or use other D-Bus interfaces.

When Operion starts, it detects that it's on a GNOME-based system and loads the `GnomeSystemMonitor` implementation. This allows the core logic in the Controller to remain completely platform-agnostic.

## Extensibility

This pluggable architecture makes it easy to extend Operion's capabilities.

-   **Supporting New OSes:** To support a new OS (e.g., a new Linux desktop environment), a developer only needs to create a new class that implements the `SystemMonitor` interface. They don't need to understand the core logic of the Controller.
-   **Adding New Hooks:** If we want to add a new feature, like monitoring microphone usage, we can simply add a `get_microphone_usage()` method to the interface and implement it for each platform.

This design isolates the most complex and fragile part of the system (the OS interaction) into well-contained, swappable modules.
