# Critique: Initial Documentation (2026-01-17)

**Verdict: Unusable for Engineering.**

The current documentation state (as of Jan 17, 2026) is a failure of technical communication. It reads like a pitch deck designed to separate a venture capitalist from their money, not a specification designed to help an engineer build a system.

It is bloated with philosophy, repetitive in the extreme, and dangerously vague on actual implementation details.

## 1. Tone: Stop Selling, Start Specifying

**The Problem:** The documentation is saturated with marketing fluff.
-   **Offenders:** `docs/0100_introduction.md`, `docs/features/0100_modes.md`, `docs/features/0900_ai_productivity_coach.md`.
-   **Evidence:** Phrases like "A Reflective Partner in Your Productivity Journey," "The Psychology of Color," "Guilt-free consumption."
-   **Impact:** This is noise. A developer does not need to be convinced *why* a feature is emotionally resonant. They need to know *what* the feature does, *how* it handles edge cases, and *where* the data lives. The emotional justification belongs in a `VISION.md` or a blog post, not in the technical specs.

**The Fix:**
-   Delete every sentence that explains "why" unless it directly impacts architectural constraints.
-   Delete the entire "Psychology of Color and Light" section in `0400_ui_themes.md`. It is irrelevant to the code.

## 2. Architecture: "Hand-Waving" is Not Design

**The Problem:** The architecture documents rely on "conceptual" examples and "conceptual" interfaces. This is lazy.
-   **Offender:** `docs/architecture/0300_system_hooks_and_monitors.md`.
    -   It claims: "It will subscribe to focus change events on the D-Bus bus."
    -   **CRITICAL FAILURE:** *Which* D-Bus interface? `org.gnome.Shell`? `org.a11y.atspi`? `org.freedesktop.impl.portal.Request`? Is this running on the Session bus or System bus?
    -   The difference between "we will use D-Bus" and "we will listen to signal `ActiveWindowChanged` on `org.gnome.Shell`" is the difference between a daydream and a plan.
-   **Offender:** `docs/architecture/0600_storage_and_data.md`.
    -   "Database Schema (Conceptual)". Stop conceptualizing. Write the SQL.
    -   Are we using foreign keys? Indices? What is the migration strategy? "Conceptual" schemas are useless for implementation.

**The Fix:**
-   Define the **exact** D-Bus interfaces (names, paths, methods, signatures).
-   Define the **exact** SQL schema (`CREATE TABLE` statements).
-   Define the **exact** file paths (`$XDG_CONFIG_HOME/operion/modes.yaml`, not `~/.config/...`).

## 3. Organization: The "Feature vs. Architecture" Fallacy

**The Problem:** The documentation splits `architecture/` and `features/` in a way that creates massive redundancy.
-   **Evidence:**
    -   "Modes" are defined in `docs/0100_introduction.md`.
    -   "Modes" are defined in `docs/architecture/0200_operion_controller.md`.
    -   "Modes" are defined in `docs/features/0100_modes.md`.
-   **Impact:** This guarantees documentation drift. If we change how a mode works (e.g., adding a `soundscape` property), we now have to update three different files. One of them *will* be forgotten, leading to conflicting specs.

**The Fix:**
-   Merge these. A feature *is* its architecture.
-   `0100_modes.md` should contain the user definition AND the struct definition AND the config schema.

## 4. Feature Creep: Science Fiction is Not Scope

**The Problem:** The documentation mixes MVP requirements with pie-in-the-sky research projects.
-   **Offenders:** `docs/features/1000_mental_fatigue_detection.md`, `docs/features/0700_smart_mode_transitions.md`.
-   **Evidence:** "Potential signals could include..."
-   **Impact:** This is confusing for a developer. Am I implementing this? Is this part of the core loop? Or is this just an idea you had in the shower? Mixing "we might do this one day" with "this is how the app works" makes the scope impossible to define.

**The Fix:**
-   **Delete** the entire `stretch_goals` folder.
-   **Delete** `1000_mental_fatigue_detection.md`.
-   **Delete** `0700_smart_mode_transitions.md`.
-   Move these to a single `ROADMAP.md` file and get them out of the active documentation.

## 5. Missing Fundamentals

**The Problem:** For all the text about "Psychology" and "AI Coaching," the most basic engineering requirements are missing.
-   **Where is the Build Guide?** No `docs/development_setup/0100_getting_started.md`.
    -   What system libraries are required? (`libgtk-4-dev`, `libdbus-1-dev`, `libssl-dev`?)
    -   What is the Minimum Supported Rust Version (MSRV)?
-   **Where is the Error Handling Strategy?**
    -   What happens if `gsettings` crashes?
    -   What happens if the AI provider times out?
    -   The current docs assume the "Happy Path" everywhere.
-   **Where is the Testing Strategy?**
    -   How do we test the Activity Monitor without a full Linux GUI session?
    -   Are we mocking D-Bus?

## Summary of Required Actions

1.  **Purge the Fluff:** Delete 40% of the text. If it's not a spec, it goes.
2.  **Harden the Specs:** Replace "conceptual" examples with concrete interfaces (SQL, D-Bus introspection, Rust structs).
3.  **Consolidate:** Merge `architecture/` and `features/` to eliminate redundancy.
4.  **Scope Control:** Delete all "Stretch Goals" and "Advanced Features" that are not in the MVP.
5.  **Add Basics:** Write `BUILD.md` and `CONTRIBUTING.md`.
