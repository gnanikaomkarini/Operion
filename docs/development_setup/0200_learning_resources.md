# 0200: Learning Resources

This document provides a curated list of resources to help you get up to speed with the technologies used in Operion.

---

## 1. Rust

Rust is the core language for Operion's backend.

-   **The Rust Programming Language Book:**
    -   **Link:** [https://doc.rust-lang.org/book/](https://doc.rust-lang.org/book/)
    -   **Description:** The official and comprehensive guide to Rust. It's highly recommended to read this book cover-to-cover if you're new to Rust. It covers everything from basic syntax to advanced concepts like ownership and concurrency.
-   **Rust by Example:**
    -   **Link:** [https://doc.rust-lang.org/rust-by-example/](https://doc.rust-lang.org/rust-by-example/)
    -   **Description:** A collection of runnable examples that illustrate various Rust concepts and standard library features. Great for hands-on learning.
-   **Rustlings:**
    -   **Link:** [https://github.com/rust-lang/rustlings](https://github.com/rust-lang/rustlings)
    -   **Description:** Small exercises to get you used to reading and writing Rust code. It's a great way to practice and solidify your understanding after going through the Rust Book.

---

## 2. Tauri

Tauri is the framework used to build the desktop application and bridge between the Rust backend and the web frontend.

-   **Tauri Documentation (Official):**
    -   **Link:** [https://tauri.app/v1/guides/introduction/](https://tauri.app/v1/guides/introduction/)
    -   **Description:** The official guides provide excellent documentation on setting up a Tauri project, understanding its architecture, and using its features like commands, plugins, and IPC.
-   **Tauri API Reference:**
    -   **Link:** [https://tauri.app/v1/api/js/](https://tauri.app/v1/api/js/) (JavaScript/TypeScript)
    -   **Link:** [https://docs.rs/tauri/latest/tauri/](https://docs.rs/tauri/latest/tauri/) (Rust)
    -   **Description:** Essential for looking up specific functions and how to use them in both the frontend and backend.

---

## 3. Svelte

Svelte is the JavaScript framework used to build Operion's user interface.

-   **Svelte Tutorial (Official):**
    -   **Link:** [https://svelte.dev/tutorial](https://svelte.dev/tutorial)
    -   **Description:** The interactive official tutorial is the best way to learn Svelte from scratch. It's very well-structured and covers all core concepts.
-   **Svelte Documentation (Official):**
    -   **Link:** [https://svelte.dev/docs](https://svelte.dev/docs)
    -   **Description:** Comprehensive reference for Svelte's API and features.

---

## 4. Ollama

Ollama allows you to run large language models locally.

-   **Ollama Website:**
    -   **Link:** [https://ollama.com/](https://ollama.com/)
    -   **Description:** The main hub for Ollama. Contains installation instructions, a list of available models, and basic usage examples.
-   **Ollama GitHub Repository:**
    -   **Link:** [https://github.com/ollama/ollama](https://github.com/ollama/ollama)
    -   **Description:** The source code and a good place to look for more advanced usage, community discussions, and troubleshooting.

---

## 5. SQLite with Rust (`rusqlite` crate)

SQLite will be used for local data storage, and `rusqlite` is the idiomatic Rust library for interacting with it.

-   **`rusqlite` Crate Documentation:**
    -   **Link:** [https://docs.rs/rusqlite/latest/rusqlite/](https://docs.rs/rusqlite/latest/rusqlite/)
    -   **Description:** The official documentation for the `rusqlite` crate. This will be your primary resource for learning how to perform database operations (connecting, querying, inserting, updating) in Rust. It includes examples.
-   **SQLite Official Documentation:**
    -   **Link:** [https://www.sqlite.org/docs.html](https://www.sqlite.org/docs.html)
    -   **Description:** While `rusqlite` handles the Rust-specifics, understanding the core SQLite SQL syntax and concepts is crucial.
