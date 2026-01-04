# 0300: System Hooks & Monitors

## The Bridge to the Operating System

The **System Hooks & Monitors** are the components that interact directly with the underlying operating system. They are the "hands and eyes" of Operion, responsible for gathering information about the system and executing the commands issued by the **Operion Controller**.

This layer is inherently OS-specific. The way you get the active window title on Linux is different from how you do it on Windows or macOS. Therefore, this entire component is designed as a **pluggable interface**.

## The Interface-Driven Design

The Controller does not talk to any specific OS-level API. Instead, it talks to a generic `SystemMonitor` interface.

This interface defines a set of methods that every platform-specific implementation must provide.

### `SystemMonitor` Interface (Conceptual):

```python
class SystemMonitor:
    """An interface for OS-specific monitoring and control."""

    def get_active_window_info(self) -> dict:
        """Returns info about the foreground window, e.g., {'app_name': '...', 'window_title': '...'}."""
        pass

    def get_running_apps(self) -> list[str]:
        """Returns a list of running application names."""
        pass

    def block_app(self, app_name: str) -> bool:
        """Blocks or hides an application. Returns True on success."""
        pass

    def set_system_theme(self, theme_name: str):
        """Sets the system UI theme (e.g., 'light', 'dark')."""
        pass

    def start_monitoring(self, event_queue: Queue):
        """Begins monitoring the system for events and puts them into the provided queue."""
        pass
```

## Pluggable Implementations

For each supported operating system, we will create a concrete implementation of this interface.

-   `LinuxSystemMonitor`: Might use libraries like `python-xlib` or D-Bus to interact with the X11 or Wayland display servers.
-   `WindowsSystemMonitor`: Will use the `pywin32` library to interact with the Windows API (e.g., `GetForegroundWindow`, `EnumWindows`).
-   `MacosSystemMonitor`: Will use the `pyobjc` bridge to access macOS's AppKit and other native frameworks.

When Operion starts, it detects the current operating system and loads the appropriate `SystemMonitor` implementation. This allows the core logic in the Controller to remain completely platform-agnostic.

## Extensibility

This pluggable architecture makes it easy to extend Operion's capabilities.

-   **Supporting New OSes:** To support a new OS (e.g., a new Linux desktop environment), a developer only needs to create a new class that implements the `SystemMonitor` interface. They don't need to understand the core logic of the Controller.
-   **Adding New Hooks:** If we want to add a new feature, like monitoring microphone usage, we can simply add a `get_microphone_usage()` method to the interface and implement it for each platform.

This design isolates the most complex and fragile part of the system (the OS interaction) into well-contained, swappable modules.
