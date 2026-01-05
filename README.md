# Operion 🧠⚙️  
**An Intent-Aware Operating System Layer for Focused Living**

Operion is a mode-driven, intelligent operating system *experience* that adapts your digital environment based on **intent, time, and behavior**.

Instead of treating all apps and activities equally, Operion introduces system-wide **modes** that reshape your UI, control app access, and guide user behavior using AI-powered insights — helping you work deeply, rest intentionally, and consume entertainment mindfully.

Operion is built as a lightweight operating layer on top of an existing OS, with an initial focus on **Linux**.

---

## ✨ Why Operion?

Modern operating systems optimize for performance — not humans.

Operion optimizes for:
- Focus without friction
- Intentional mode switching
- Behavioral awareness
- Sustainable productivity

> Operion doesn’t ask for discipline.  
> It designs the system around it.

---

## 🧠 Core Concepts: Modes

Operion's power comes from its system-wide **modes**. Instead of a one-size-fits-all desktop, you can instantly switch between different environments, each with its own rules and purpose.

- **🧑‍💻 Work Mode:** A distraction-free environment for deep focus.
- **😌 Chill Mode:** For light productivity and mental recovery.
- **🎬 Entertainment Mode:** For intentional, guilt-free leisure.
- **⚡ Focus Sprint Mode:** A temporary, high-intensity, single-tasking mode for short bursts of deep work, inspired by the Pomodoro Technique.
- **🚫 Suspended Mode:** A "hands-off" mode that completely pauses all of Operion's features, guaranteeing zero interference.
- **✨ Custom Modes:** Create your own modes from scratch (e.g., "Study," "Design," "Reading") with their own specific rules, apps, and UI themes.

---

## ✨ Core Features

- **Intelligent Browser Protection:** A companion browser extension that understands the content you're viewing. During `Work Mode`, it automatically blurs distracting websites, forcing you to stay on task without needing to block the entire browser.
- **Task-Driven Calendar:** Integrate your to-do list with the calendar. Link specific tasks to your `Work Mode` blocks and get a gentle, passive reminder of your current objective.
- **App & Website Control:** Go beyond browser protection with system-wide application whitelists/blacklists tailored to each mode.
- **Session Review Journaling:** At the end of a work session, Operion prompts you for a quick reflection on your accomplishments and challenges, adding powerful qualitative context to your analytics.
- **AI Productivity Coach:** At the end of the day, receive a personalized summary that compares your goals with your actual results, providing actionable advice for the next day.
- **Privacy-First Activity Monitoring:** Understand how you spend your time with a local-only activity monitor. No data ever leaves your machine.

---

## 🧰 Tech Stack

Operion is built with a modern, high-performance, and privacy-focused tech stack.

- **Core Language:** **Rust** — For a memory-safe, high-performance, and lightweight backend.
- **UI Framework:** **Tauri** with **Svelte** — To create a beautiful, fast, and resource-efficient desktop UI using web technologies.
- **AI Engine:** **Ollama** — To run powerful open-source language models locally, ensuring zero cost and 100% privacy.
- **Database:** **SQLite** — For robust, local, and file-based data storage.

---

## 🚀 Getting Started

This project is in the early stages of development. All documentation is located in the `/docs` directory.

1.  **Learn the Architecture:** To understand how Operion works, start by reading the documents in `docs/architecture`.
2.  **Set up your Environment:** Follow the `docs/development_setup/0100_installation_guide.md` to configure your Linux development environment.
3.  **Learn the Technologies:** If you're new to the tech stack, check out the curated list of tutorials and guides in `docs/development_setup/0200_learning_resources.md`.

---
## 🛠️ Architecture Overview
```text
+---------------------------+
|        Operion UI         |
|   (Tauri + Svelte)        |
+---------------------------+
            | (Tauri IPC)
+---------------------------+
|     Operion Controller    |
|   (Rust Core Logic)       |
+---------------------------+
            | (System Events)
+---------------------------+      +---------------------------+
|   System Hooks & Monitors |----->|     AI Insight Engine     |
|   (Rust, OS-specific)     |      |   (Ollama Integration)    |
+---------------------------+      +---------------------------+
```