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

## 2. GNOME Desktop Integration

To achieve deep OS integration on Zorin OS, Operion interacts directly with the GNOME desktop environment. This is done primarily through D-Bus and system command-line tools.

-   **The `zbus` Crate for D-Bus:**
    -   **Link:** [https://docs.rs/zbus/latest/zbus/](https://docs.rs/zbus/latest/zbus/)
    -   **Description:** `zbus` is a modern, async-first Rust library for D-Bus, the standard IPC system used by GNOME and most Linux desktops. This is the key technology for sending native notifications, interacting with the system tray, and communicating between Operion's components. The `zbus` book is an excellent place to start.
-   **GNOME `gsettings` Command:**
    -   **Link:** [https://developer.gnome.org/documentation/tutorials/settings.html](https://developer.gnome.org/documentation/tutorials/settings.html)
    -   **Description:** `gsettings` is a command-line tool for viewing and changing user settings in GNOME. Operion uses this to change the GTK theme, icon theme, wallpaper, and other desktop appearance settings. A good understanding of the GNOME settings schemas (e.g., `org.gnome.desktop.interface`) is essential.
-   **GNOME Shell Extensions:**
    -   **Link:** [https://gjs.guide/extensions/](https://gjs.guide/extensions/)
    -   **Description:** While Operion's core is Rust, the panel applet itself will likely be a small GNOME Shell Extension written in JavaScript. This guide is the best resource for learning how to create and manage extensions that add new icons and menus to the GNOME panel.

---

## 3. Ollama

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
