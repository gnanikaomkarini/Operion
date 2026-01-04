# 0600: Storage and Data Management

## A Clear Separation of Data and Configuration

Operion's storage layer is designed to be simple, robust, and privacy-focused. It is built on a fundamental principle: a clear separation between **user configuration** and **activity data**.

-   **User Configuration:** These are the human-readable files that define how Operion should behave (e.g., `modes.yaml`). The user is expected to directly view and edit these files. They define the *rules*.
-   **Activity Data:** This is the time-series data collected by the Activity Monitor (e.g., what app was used and when). This data is stored in a structured, machine-readable format and is not meant to be edited by the user directly. It represents the *history* of what happened.

This separation ensures that the user's settings are easy to manage and back up, while the application's historical data can be stored efficiently.

## User Configuration

-   **Format:** Human-readable text files, such as YAML or TOML. This makes them easy to edit with any text editor.
-   **Location:** A standard user configuration directory, e.g., `~/.config/operion/`.
-   **Content:** This includes the definition of modes, application and website blacklists/whitelists, and settings for the AI engine.

**Example `config.yaml`:**
```yaml
ai:
  provider: "gemini" # 'gemini', 'openai', or 'local'
  api_key: "..." # Loaded from environment variable

ui:
  theme: "system"
```

## Activity Data

The activity data is stored in a local **SQLite database**. SQLite is a perfect choice for this use case because it is serverless, self-contained, and creates a single database file that is easy to manage and back up.

-   **Location:** A standard user data directory, e.g., `~/.local/share/operion/activity.db`.
-   **Privacy:** The database file is stored locally and never leaves the user's machine.

### Database Schema (Conceptual)

The database schema is designed to be simple and efficient for time-series analysis.

**`activity_log` Table:**
-   `id` (INTEGER, PRIMARY KEY): A unique ID for each entry.
-   `timestamp` (INTEGER): A Unix timestamp of when the event occurred.
-   `app_name` (TEXT): The name of the application in the foreground (e.g., "Code").
-   `window_title` (TEXT): The title of the active window.
-   `mode` (TEXT): The active Operion mode at the time of the event (e.g., "work").
-   `duration` (INTEGER): The number of seconds the app was in the foreground before the state changed.

**`mode_log` Table:**
-   `id` (INTEGER, PRIMARY KEY): A unique ID for each entry.
-   `timestamp` (INTEGER): A Unix timestamp of when the mode switch occurred.
-   `new_mode` (TEXT): The mode that was switched to (e.g., "chill").
-   `previous_mode` (TEXT): The mode that was switched from.

This simple schema allows Operion to efficiently query the database to generate all the insights and analytics, such as calculating the time spent in each mode or identifying the most used applications.
