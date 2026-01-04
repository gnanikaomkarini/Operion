# 0100: Architectural Overview

## Guiding Principles

The architecture of Operion is designed around three core principles:

1.  **Modularity:** Each major component of the system should be independent and communicate with other components through well-defined interfaces. This allows for easier development, testing, and maintenance. It also allows for parts of the system to be replaced or extended by the user or community.
2.  **Extensibility:** The system should be easy to extend with new features, new integrations, or support for new operating systems. This is crucial for building a vibrant community around the project.
3.  **User-Centric Configuration:** The user should have full control over their experience. The system should not impose a rigid, one-size-fits-all definition of "productivity." All rules, policies, and settings should be easily configurable by the user through simple files.

## The High-Level Architecture

Operion consists of several key components that work together to create the full experience.

```text
+---------------------------+
|        Operion UI         |
|  (Mode Switch, Dashboard) |
+---------------------------+
            | (IPC / API)
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

-   **Operion UI:** The graphical front-end for the user. It is responsible for displaying the current mode, allowing the user to switch modes, and presenting the insights and analytics. It is a "dumb" client that gets its state and data from the Controller.
-   **Operion Controller:** The "brain" of the system. It runs as a background process (or daemon). It reads the user's configuration, maintains the system's current state (i.e., the active mode), and issues commands to the other components.
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
