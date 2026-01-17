# 1000: AI Productivity Coach

## Feature Scope

The AI Productivity Coach generates a text summary of daily activity using a local Large Language Model (LLM).

## Architecture

1.  **Data Aggregation:** The Controller queries the `activity_log` SQLite table for the last 24 hours.
2.  **Prompt Engineering:** A structured prompt is constructed, containing:
    -   Total time in "Work" mode.
    -   Top 3 applications by duration.
    -   Count of context switches.
3.  **Inference:** The prompt is sent to a local Ollama instance.
4.  **Delivery:** The response is displayed as a persistent system notification.

## Interface

The Controller communicates with the AI service (Ollama) via HTTP.

-   **Endpoint:** `http://localhost:11434/api/generate`
-   **Model:** Defaults to `llama3` (configurable).

## Privacy Constraints

-   All inference runs on `localhost`.
-   Window titles are sanitized (potentially sensitive info removed) before being inserted into the prompt.
-   No data is transmitted to external APIs.