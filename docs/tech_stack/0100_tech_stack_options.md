# 0100: Tech Stack Options & Recommendations

This document outlines the various technology choices available for building Operion, provides a recommendation for each category, and explains the reasoning.

---

## 1. Core Language (Backend & Controller)

This is the language for the main application logic, controller, system hooks, and database interactions.

### Tabular Comparison

| Criteria              | Python                               | **Rust (Recommended)**                 | Go                                     |
| --------------------- | ------------------------------------ | -------------------------------------- | -------------------------------------- |
| **Performance**       |  низкой                           | **Excellent**                          | Good                                   |
| **Memory Usage**      | High                                 | **Very Low**                           | Low                                    |
| **Safety**            | Okay (Dynamically Typed)             | **Excellent (Compile-time)**           | Good (Garbage Collected)               |
| **Learning Curve**    | Easy                                 | **Hard**                               | Medium                                 |
| **AI/ML Ecosystem**   | Excellent                            | **Good & Growing**                     | Fair                                   |
| **UI Framework Synergy** | Poor                                 | **Excellent (with Tauri)**             | Poor                                   |
| **Best For**          | Rapid Prototyping, AI tasks          | **Performant & Safe System Utilities** | Network Services, CLI tools            |

### Options Analysis

#### Option A: Python
-   **Description:** A high-level, interpreted language known for its ease of use and extensive library support.
-   **Pros:** Unmatched AI ecosystem, easy to learn, mature libraries for OS interaction.
-   **Cons:** Significantly slower and more memory-intensive than compiled alternatives, which is a major drawback for a lightweight system utility.

#### Option B: Rust
-   **Description:** A modern, compiled language focused on performance, memory safety, and concurrency.
-   **Pros:** Elite performance, guaranteed memory safety, first-class tooling, and perfect synergy with the Tauri UI framework.
-   **Cons:** Steep learning curve, development can be slower than in Python.

#### Option C: Go
-   **Description:** A simple, compiled language from Google, known for its excellent concurrency support.
-   **Pros:** Much easier to learn than Rust, great for concurrent tasks, compiles quickly to a single binary.
-   **Cons:** Less synergy with UI frameworks and its ecosystem for low-level system hooks is less mature than Rust's.

### Recommendation: Rust

**Rust is the clear winner for Operion.** While it has a steeper learning curve, the benefits are immense and directly address the project's core requirements. For a tool that runs constantly in the background and interacts with the OS, performance and memory safety are paramount. Rust provides this without compromise. Most importantly, its seamless integration with Tauri allows us to build the *entire* application—backend, frontend, and build process—within a single, cohesive, and modern ecosystem. This is a decisive advantage that no other language can offer for this project.

---

## 2. UI Framework

This technology will be used to build the user interface (dashboard, widgets, etc.).

### Tabular Comparison

| Criteria          | **Tauri (Recommended)**          | Electron                         |
| ----------------- | -------------------------------- | -------------------------------- |
| **Performance**   | **Excellent**                    | Fair                             |
| **Resource Usage**| **Very Low**                     | High                             |
| **App Size**      | **Very Small (~2-10 MB)**        | Large (~50-100 MB+)              |
| **Maturity**      | Good & Growing                   | **Excellent**                    |
| **Best For**      | **Lightweight Desktop Apps**     | Complex, feature-rich apps       |

### Options Analysis

#### Option A: Tauri (with Svelte/React/Vue)
-   **Description:** A framework for building native desktop apps using web technologies by leveraging the OS's native webview.
-   **Pros:** Extremely lightweight, high performance, produces tiny app bundles, and has powerful features for creating overlay-style UIs.
-   **Cons:** Requires knowledge of both web development and Rust (if Rust is the chosen core language).

#### Option B: Electron (with Svelte/React/Vue)
-   **Description:** The original framework for this purpose (used by VS Code, Slack), which bundles a full Chromium browser.
-   **Pros:** Very mature, stable, and easy to get started with.
-   **Cons:** High resource usage and large app size are directly contrary to Operion's goal of being a "lightweight layer".

### Recommendation: Tauri

**Tauri is the ideal choice.** Its philosophy aligns perfectly with Operion's. It delivers the smallest, fastest, and most resource-efficient application possible while still allowing for a beautiful, modern UI to be built with web technologies. Your vision of "overlaying the actual layout of the system" is perfectly served by Tauri's support for transparent, borderless, multi-window applications. The cost of learning the Tauri/Rust integration is a small price to pay for such a massive gain in performance and efficiency.

---

## 3. AI Engine

This component will classify content and provide intelligent suggestions.

### Tabular Comparison

| Criteria                  | **Local LLM (Ollama) (Recommended)** | Cloud LLM (Gemini, etc.)   |
| ------------------------- | ------------------------------------ | -------------------------- |
| **Cost**                  | **Free**                             | Potentially Expensive      |
| **Privacy**               | **Excellent (100% Local)**           | Poor (Data sent to cloud)  |
| **Offline Capability**    | **Yes**                              | No                         |
| **User Setup**            | Manual Installation Required         | **Easy (API Key)**         |
| **Performance**           | Hardware Dependent                   | **Fast & Consistent**      |
| **Quality**               | Good to Very Good                    | State-of-the-art           |

### Options Analysis

#### Option A: Local LLM (via Ollama)
-   **Description:** The user installs and runs an open-source LLM locally via the Ollama tool. Operion communicates with the local Ollama server.
-   **Pros:** Completely free, 100% private, and works offline.
-   **Cons:** Requires manual setup by the user and performance is dependent on the user's hardware.

#### Option B: Cloud LLM (Gemini, OpenAI, etc.)
-   **Description:** Operion sends API requests to a commercial AI service.
-   **Pros:** Highest quality responses and easy setup for the user (just an API key).
-   **Cons:** Can be expensive, requires an internet connection, and involves privacy trade-offs.

### Recommendation: Local LLM (Ollama)

**Ollama is the right choice given your "free forever" constraint.** It completely eliminates cost concerns and provides the strongest possible privacy guarantees for the user, which is a huge selling point for an app that monitors user activity. While it requires a one-time setup for the user, this is a reasonable trade-off. We can provide clear instructions for this setup. The performance and quality of local models are improving at an incredible pace, making this a sustainable and future-proof decision.

---

## 4. Database

This is where the application will store historical activity data.

### Tabular Comparison

| Criteria            | **SQLite (Recommended)**     | Plain Text Files (JSON/CSV) |
| ------------------- | ---------------------------- | --------------------------- |
| **Query Performance** | **Excellent**                | Very Poor                   |
| **Reliability**     | **Excellent (Transactional)**| Fair (Prone to corruption)  |
| **Ease of Use**     | Excellent                    | Deceptively Complex         |

### Recommendation: SQLite

This is the most straightforward decision. **SQLite is the only professional choice here.** It is purpose-built for this exact scenario. It is fast, transactional (meaning data won't be corrupted if a write is interrupted), and has rock-solid library support in every major language. The "human-readability" of plain text files is a false economy that would quickly lead to massive performance and reliability problems.