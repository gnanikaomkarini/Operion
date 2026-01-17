# 200: System Modes (Specification)

## Definition

A "Mode" is a named configuration state that dictates system behavior. Modes are defined in the user's configuration file (`modes.toml`).

## Configuration Schema

Modes are defined in TOML. The daemon watches this file for changes and hot-reloads the configuration.

```toml
# ~/.config/operion/modes.toml

[modes.work]
name = "Deep Work"
theme = "Adwaita-dark"
wallpaper = "file:///home/user/wallpapers/focus.jpg"
policy = "whitelist"
apps = ["code", "firefox", "gnome-terminal"]
blocks_notifications = true

[modes.chill]
name = "Relaxation"
theme = "Adwaita" # Light theme
policy = "blacklist"
apps = ["slack", "discord"] # Block work comms
```

## Mode Attributes

| Attribute | Type | Description |
| :--- | :--- | :--- |
| `name` | `string` | Display name for the UI. |
| `theme` | `string` | GTK theme name (must be installed on host). |
| `wallpaper` | `string` | Absolute URI to the wallpaper image. |
| `policy` | `enum` | `whitelist` (allow only listed) or `blacklist` (block listed). |
| `apps` | `Vec<string>` | List of binary names or app IDs. |
| `blocks_notifications` | `bool` | If true, enables Do Not Disturb (DND). |

## Default Modes

The system ships with three default definitions if the config file is missing:
1.  **Work:** Whitelist-based, dark theme, DND enabled.
2.  **Chill:** Blacklist-based (blocks productivity apps), light theme.
3.  **Entertainment:** Unrestricted.