# 0100: Architectural Overview

## Guiding Principles

The architecture of Operion is designed around three core principles:

1.  **Modularity:** Each major component of the system should be independent and communicate with other components through well-defined interfaces. This allows for easier development, testing, and maintenance. It also allows for parts of the system to be replaced or extended by the user or community.
2.  **Extensibility:** The system should be easy to extend with new features, new integrations, or support for new operating systems. This is crucial for building a vibrant community around the project.
3.  **User-Centric Configuration:** The user should have full control over their experience. The system should not impose a rigid, one-size-fits-all definition of "productivity." All rules, policies, and settings should be easily configurable by the user through simple files.

## The High-Level Architecture

Operion consists of several key components that work together to create an experience that is deeply integrated with the host operating system.

```text
+--------------------------------+
| Desktop Environment (GNOME)    |
| (Panel Applet, Notifications)  |
+--------------------------------+
     ^      | (D-Bus / Commands)
     | (User Input)
+---------------------------+
|     Operion Controller    |
| (Rules, Policies, Modes)  |
+---------------------------+
            | (Events / Commands)
+---------------------------+      +---------------------------+
|   System Hooks & Monitors |----->|     AI Insight Engine     |
| (Apps, Windows, Activity) |      | (Classification & Advice) |
+---------------------------+      +---------------------------+
            | (Data)
+---------------------------+
|          Storage          |
|   (SQLite, Config Files)  |
+---------------------------+
```

### Component Responsibilities:

-   **Desktop Environment Integration:** This is not a component we build, but the user's existing desktop environment (initially Zorin OS/GNOME) that we interact with. Operion's "UI" consists of native elements like a panel applet for mode switching and system notifications for feedback. All interactions are handled through OS-native mechanisms.
-   **Operion Controller:** The "brain" of the system. It runs as a background process (or daemon). It reads the user's configuration, maintains the system's current state (i.e., the active mode), and issues commands to the other components (e.g., telling a System Hook to block an app, or telling the Desktop Environment to change the theme).
-   **System Hooks & Monitors:** A set of OS-specific modules that interact directly with the operating system. They are responsible for tasks like:
    -   Getting the list of running applications.
    -   Identifying the active window and its title.
    -   Blocking or hiding applications.
    -   Changing system UI themes.
-   **AI Insight Engine:** A component that processes the data collected by the Monitors to provide higher-level insights. This is where features like Content Awareness and the AI Productivity Coach are implemented.
-   **Storage:** The component responsible for persisting data. This includes:
    -   User configuration files (e.g., in YAML or TOML format).
    -   The SQLite database for storing time-series activity data.

The following documents in this section will explore each of these components in greater detail.

---

### Practical Example

To see how these components work together in a real-world scenario, refer to the **[0800: Interaction Workflow](./0800_interaction_workflow.md)** document for a detailed breakdown of a manual mode switch.
