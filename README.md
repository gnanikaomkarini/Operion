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

## 🧠 Core Concept: Modes

Operion introduces **system-wide modes** that define *how* and *why* your computer behaves at any moment.

- **🧑‍💻 Work Mode:** A distraction-free environment for deep focus.
- **😌 Chill Mode:** For light productivity and mental recovery.
- **🎬 Entertainment Mode:** For intentional, guilt-free leisure.

---

## ✨ Core Features

- **App Control & Restrictions:** Whitelist or blacklist applications and websites based on the current mode.
- **Activity Monitoring:** Understand how you spend your time with local, privacy-first activity tracking.
- **AI-Powered Content Awareness:** Uses a local AI to classify content (not just apps) to provide more accurate focus scoring.
- **Insights & Analytics:** Get actionable insights into your focus, productivity, and distraction patterns.
- **Calendar-Driven Mode Locking:** Plan your day on a calendar and have Operion automatically lock you into modes to enforce your intentions.
- **AI Productivity Coach:** Receive a personalized, reflective summary of your day with suggestions for improvement.

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