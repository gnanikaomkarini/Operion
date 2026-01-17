# 100: Introduction to Operion

## Overview

Operion is a mode-driven operating system layer for Linux (specifically GNOME/Wayland environments). It acts as a system controller that modifies the desktop environment state—application permissions, UI themes, and notification policies—based on a user-defined "Mode".

It is implemented as a Rust daemon (`operiond`) communicating with the GNOME Shell via D-Bus and GSettings.

## Core Capabilities

-   **State Management:** Enforces system-wide states (Modes) like "Work" or "Chill".
-   **Process Control:** Monitors running processes and terminates those restricted by the active mode.
-   **Visual Feedback:** Switches GTK themes and wallpapers to match the active context.
-   **Telemetry:** Logs window focus events to a local SQLite database for analytics.

## System Architecture

Operion operates as a user-space daemon.

```text
[Operion Daemon] <--- D-Bus ---> [GNOME Shell Extension]
       |
       +--- [GSettings] (Theme Control)
       |
       +--- [SQLite] (Activity Log)
       |
       +--- [Config File] (~/.config/operion/modes.toml)
```