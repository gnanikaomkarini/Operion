# 0800: Interaction Workflow: Manual Mode Switching

This document provides a concrete, step-by-step example of how Operion's architectural components work together to fulfill a core user action: manually switching modes from the desktop panel.

This workflow involves two primary components:
-   **The GNOME Shell Extension (Frontend):** A lightweight piece of JavaScript that provides the UI element in the top panel.
-   **The Operion Controller (Backend):** The persistent Rust service that contains all application logic.

They communicate using **D-Bus**, the native Inter-Process Communication (IPC) system for the GNOME desktop.

---

### The Workflow Diagram

```
User         GNOME Shell Extension         D-Bus          Operion Controller (Rust)       Desktop (gsettings, etc.)
 │                   │                      │                       │                           │
 │  clicks icon     │                      │                       │                           │
 │──────────────────>│                      │                       │                           │
 │                   │ asks for modes       │                       │                           │
 │                   │─────────────────────>│ gets modes/state      │                           │
 │                   │                      │<──────────────────────│                           │
 │                   │<─────────────────────│                       │                           │
 │ builds menu       │                      │                       │                           │
 │<──────────────────│                      │                       │                           │
 │                   │                      │                       │                           │
 │ clicks "Work"     │                      │                       │                           │
 │──────────────────>│                      │                       │                           │
 │                   │ sends "setMode" cmd  │                       │                           │
 │                   │─────────────────────>│ setMode("Work")       │                           │
 │                   │                      │──────────────────────>│                           │
 │                   │                      │                       │ Executes Rules...         │
 │                   │                      │                       │──────────────────────────>│ changes theme
 │                   │                      │                       │──────────────────────────>│ changes wallpaper
 │                   │                      │                       │                           │
 │                   │                      │   "modeChanged" event │                           │
 │                   │                      │<──────────────────────│                           │
 │                   │<─────────────────────│                       │                           │
 │ updates icon      │                      │                       │                           │
 │<──────────────────│                      │                       │                           │
 │                   │                      │                       │                           │
```

---

### Step 1: Startup & Initial State

1.  **Backend Starts:** When the user logs in, the `Operion Controller` Rust service is started via `systemd` or a similar mechanism. It reads the `modes.yaml` config file and determines the initial system mode.
2.  **Frontend Starts:** The GNOME Shell loads all enabled extensions, including the Operion panel applet.
3.  **Initial Sync:** The extension's JavaScript code immediately makes a D-Bus call to the `Operion Controller` to ask for the current mode. Based on the reply, it sets the appropriate icon in the top panel.

### Step 2: User Clicks the Panel Icon

1.  **Click Event:** The user clicks the Operion icon. This triggers the extension's menu-building function.
2.  **Menu Request:** The extension makes two D-Bus calls to the `Operion Controller`:
    -   `getAvailableModes()`
    -   `getCurrentMode()`
3.  **Backend Response:** The Rust service responds with the list of all mode names from the configuration, and the name of the currently active mode.
4.  **Menu Building:** The extension's JavaScript code dynamically populates a menu with the list of modes, placing a checkmark or other indicator next to the active one.

### Step 3: User Selects a New Mode

1.  **New Selection:** The user clicks a different mode in the menu, for example, "Work".
2.  **Command Sent:** The extension's JavaScript code captures this selection and makes a single D-Bus call to the `Operion Controller`: `setMode("Work")`.

### Step 4: Backend Executes the Mode Change

1.  **Command Received:** The Rust service receives the `setMode("Work")` command.
2.  **Logic Execution:** The Controller now consults its parsed configuration for the rules associated with "Work Mode". It begins executing these rules sequentially:
    -   It dispatches a command to change the GTK theme via `gsettings`.
    -   It dispatches another command to change the desktop wallpaper.
    -   It queries the `SystemMonitor` for a list of running processes and compares it against the application policy for "Work Mode", terminating any forbidden applications.
3.  **State Update:** Once all actions are successfully completed, the Controller updates its internal state to reflect that "Work" is now the active mode.

### Step 5: UI Feedback Loop

1.  **Event Broadcast:** The `Operion Controller` broadcasts a `ModeChanged` signal over D-Bus, containing the name of the new mode ("Work").
2.  **Icon Update:** The GNOME Shell extension is always listening for this signal. When it receives it, it runs its icon update logic, changing the icon in the panel to the one specified for "Work Mode".

This completes the entire interaction, providing a responsive and native-feeling experience while keeping the UI and core logic cleanly separated.
