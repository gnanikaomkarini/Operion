# 900: AI Content Awareness

## Window Title Classification

This module classifies ambiguous activities (like "Browser") based on window titles.

## Pipeline

1.  **Trigger:** `ActiveWindowChanged` event where `app_id` is a browser.
2.  **Extraction:** Get window title (e.g., "Advanced Rust Traits - YouTube").
3.  **Inference:** Call local LLM (Ollama) with classification prompt.
    -   *Input:* "Classify: 'Advanced Rust Traits - YouTube'"
    -   *Output:* "Category: Education"
4.  **Action:** Update `ActivityRecord` metadata (used for Focus Score).

## Caching

Results are cached (LRU Cache) by Title Hash to minimize LLM latency.