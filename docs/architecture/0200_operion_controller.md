# 0200: The Operion Controller

## The Central Nervous System

The **Operion Controller** is the core component of the entire system. It runs as a persistent background process and acts as the central coordinator for all of Operion's functionality.

Its primary responsibilities are:

1.  **Configuration Management:** Loading, parsing, and managing the user's configuration files.
2.  **State Management:** Maintaining the current state of the system, most importantly the active mode.
3.  **Event Handling:** Listening for events from the System Hooks & Monitors (e.g., "user opened a new application") and the UI (e.g., "user requested to switch to Work Mode").
4.  **Rule Enforcement:** Applying the rules defined in the user's configuration to the current state and issuing commands accordingly.

## Configuration at the Core

Modularity and user-friendliness start with configuration. The Controller is designed to read its entire configuration from a set of simple, human-readable files (e.g., YAML or TOML format) stored in a well-known user directory (e.g., `~/.config/operion/`).

### Example Configuration:

A user could define their modes and rules in a file like `modes.yaml`:

```yaml
modes:
  work:
    name: "Work Mode"
    theme: "monochrome"
    apps:
      # Whitelist: only these apps are allowed
      policy: "whitelist"
      list:
        - "Code"
        - "Terminal"
        - "Figma"
        - "Spotify" # User-added exception
    websites:
      # Blacklist: these websites are blocked
      policy: "blacklist"
      list:
        - "youtube.com"
        - "twitter.com"
        - "reddit.com"

  chill:
    name: "Chill Mode"
    theme: "solarized-dark"
    apps:
      # Blacklist: block only the most demanding apps
      policy: "blacklist"
      list:
        - "Docker"
    websites:
      policy: "none"
      list: []
```

### Handling User Modifications

This configuration-based approach directly addresses the user's need for customization. To allow Spotify in Work Mode, the user would simply edit the `modes.yaml` file and add `"Spotify"` to the `list` under `work.apps`.

The Controller is designed to watch for changes to these configuration files. When a file is saved, the Controller will automatically reload the configuration and apply the new rules without requiring a system restart.

## The Main Control Loop

The Controller operates on a continuous loop:

1.  **Load/Reload Config:** Check if the configuration files have changed. If so, load them.
2.  **Receive Events:** Ingest a queue of events from the UI and Monitors (e.g., `app_opened`, `window_title_changed`, `user_clicked_switch_mode`).
3.  **Update State:** Update the internal state based on the events (e.g., the `active_mode` is now `work`).
4.  **Evaluate Rules:** Go through the rules for the active mode and compare them against the current system state (e.g., is the newly opened app in the whitelist?).
5.  **Dispatch Commands:** If a rule is violated, dispatch a command to the appropriate System Hook (e.g., `block_app("YouTube")`). If the UI needs to be updated, send a state-change event to the UI layer.
6.  **Repeat.**

This clean separation of concerns makes the Controller a powerful yet maintainable foundation for the entire system.
