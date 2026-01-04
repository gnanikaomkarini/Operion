# 0100: Tech Stack Options

This document outlines the various technology choices available for building Operion. Each choice has its own set of advantages and disadvantages.

---

## 1. Core Language (Backend & Controller)

This is the language that will be used to write the main application logic, including the controller, system hooks, and database interactions.

### Option A: Python

-   **Description:** A high-level, interpreted language known for its ease of use and extensive library support, especially in AI/ML.
-   **Pros:**
    -   **Fastest for AI:** Unmatched ecosystem for AI and machine learning. Integrating with any kind of AI model is easiest in Python.
    -   **Easy to Learn & Write:** Simple syntax allows for rapid development and iteration.
    -   **Mature Libraries:** Robust libraries exist for OS interaction on all platforms (`pywin32`, `pyobjc`, `python-xlib`).
-   **Cons:**
    -   **Performance:** As an interpreted language, it is significantly slower and more memory-intensive than compiled languages like Rust or Go. This is a major concern for a lightweight system utility.
    -   **Distribution:** Packaging a Python app into a standalone executable can be complex and result in a large file size.

### Option B: Rust

-   **Description:** A modern, compiled language focused on performance, memory safety, and concurrency.
-   **Pros:**
    -   **Elite Performance:** Speed is on par with C++, and memory usage is low and predictable. Ideal for a system-level tool.
    -   **Memory Safety:** The compiler guarantees memory safety, preventing crashes and security vulnerabilities common in systems programming.
    -   **Excellent for UI (Tauri):** Tauri, a leading lightweight UI framework, is built on Rust. This creates a highly cohesive, unified, and performant application.
    -   **Modern Tooling:** Has a world-class build system and package manager (Cargo).
-   **Cons:**
    -   **Steep Learning Curve:** Rust's core concepts (ownership, borrowing) can be difficult for beginners to grasp.
    -   **Slower Development:** Development speed is generally slower than in Python due to the strictness of the compiler.

### Option C: Go

-   **Description:** A simple, compiled language created by Google, known for its excellent support for concurrency.
-   **Pros:**
    -   **Simplicity:** Much easier to learn than Rust.
    -   **Great Concurrency:** Built-in "goroutines" make it very easy to run background tasks concurrently.
    -   **Fast Compilation:** Compiles very quickly, and creates single, static binaries.
-   **Cons:**
    -   **System Hooks:** Interacting with low-level OS APIs is less common and can be more cumbersome than in Rust or Python.
    -   **No UI Synergy:** Does not have a clear, first-party UI framework like Rust does with Tauri.

---

## 2. UI Framework

This is the technology used to build the user interface (the dashboard, mode switcher, widgets, etc.).

### Option A: Tauri (with Svelte/React/Vue)

-   **Description:** A framework for building native desktop apps using web technologies. It uses the operating system's native webview instead of bundling a full browser.
-   **Pros:**
    -   **Extremely Lightweight:** Produces tiny application bundles and has very low RAM usage.
    -   **High Performance:** Very fast because it's a thin layer over a Rust backend.
    -   **Modern Web Tech:** Allows you to build beautiful UIs with modern frameworks like Svelte or React.
    -   **Powerful Features:** Supports transparent windows, multiple windows, and system tray icons, which are needed for "overlaying" the OS.
-   **Cons:**
    -   Requires knowledge of both web development and Rust (if you choose a Rust core).

### Option B: Electron (with Svelte/React/Vue)

-   **Description:** The original framework for building desktop apps with web tech (used by VS Code, Slack, Discord). It bundles a full version of the Chromium web browser.
-   **Pros:**
    -   **Very Mature:** Extremely stable, well-documented, and has a massive ecosystem.
    -   **Easy to Use:** If you know Node.js and web development, it's very easy to get started.
-   **Cons:**
    -   **High Resource Usage:** Famously results in large applications that consume a lot of RAM, which is against our goal of being a "lightweight layer".

---

## 3. AI Engine

This is the component that will classify content and provide intelligent suggestions.

### Option A: Local LLM (via Ollama)

-   **Description:** The user installs and runs an open-source Large Language Model (like Llama 3 or Phi-3) locally using the Ollama tool. Our application sends HTTP requests to the Ollama server running on `localhost`.
-   **Pros:**
    -   **Completely Free:** No API costs, ever.
    -   **100% Private:** No data ever leaves the user's machine.
    -   **Offline Capable:** Works without an internet connection.
-   **Cons:**
    -   **User Setup Required:** The user must install and manage Ollama and the models themselves.
    -   **Performance Dependent on Hardware:** Requires a powerful computer (especially a good GPU) for fast responses.
    -   **Lower Quality (Potentially):** The quality of the AI responses may not be as high as top-tier cloud models.

### Option B: Cloud LLM (Gemini, OpenAI, etc.)

-   **Description:** Our application sends API requests over the internet to a commercial AI service.
-   **Pros:**
    -   **Highest Quality:** Provides state-of-the-art AI capabilities.
    -   **No User Setup:** Works out-of-the-box as long as the user provides an API key.
-   **Cons:**
    -   **Costly:** Can become very expensive, which violates a core constraint.
    -   **Requires Internet:** Does not work offline.
    -   **Privacy Concerns:** Involves sending user data (e.g., window titles) to a third party.

---

## 4. Database

This is where the application will store the historical activity data.

### Option A: SQLite

-   **Description:** A self-contained, serverless, file-based SQL database engine.
-   **Pros:**
    -   **Standard Choice:** The industry standard for local application data.
    -   **Fast & Reliable:** Extremely fast for this use case.
    -   **Excellent Language Support:** Supported out-of-the-box in Python and has high-quality libraries in Rust and Go.
-   **Cons:**
    -   None for this project. It is the ideal choice.

### Option B: Plain Text Files (JSON / CSV)

-   **Description:** Storing data in a series of files, like one JSON file per day.
-   **Pros:**
    -   **Human-Readable:** Data can be easily inspected with a text editor.
-   **Cons:**
    -   **Inefficient:** Querying the data (e.g., "how much time did I spend on 'Code' last week?") becomes very slow and complex as the number of files grows.
    -   **Prone to Corruption:** More fragile than a transactional database like SQLite.
