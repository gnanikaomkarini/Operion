# 0400: The UI Layer

## A Clean and Simple User Interface

The **UI Layer** is the primary way the user interacts with Operion. Its design philosophy is to be as clean, simple, and unobtrusive as possible. It is not a complex application itself, but rather a thin client or "viewer" for the state managed by the **Operion Controller**.

The UI has three main responsibilities:

1.  **Displaying State:** Showing the current mode, the time remaining in a locked session, and key insights.
2.  **Capturing User Intent:** Providing controls (e.g., buttons or menu items) that allow the user to request a mode change.
3.  **Presenting Data:** Displaying the analytics and suggestions from the AI Coach in a clean, readable format.

## Decoupling the UI from the Core Logic

A critical architectural decision is to keep the UI layer "dumb." This means the UI does not contain any business logic. It doesn't know what "Work Mode" is, what the rules are, or how to block an app. It only knows how to display the information it is given and how to forward user actions to the Controller.

This decoupling is achieved through a well-defined communication channel between the UI process and the background Controller process.

### Communication Channel

The recommended approach is to use a simple Inter-Process Communication (IPC) mechanism, such as a local WebSocket server or a REST-like API exposed by the Controller on a local port.

-   **Controller -> UI (Push):** The Controller sends messages to the UI whenever the state changes.
    -   `{'type': 'STATE_UPDATE', 'payload': {'current_mode': 'work', 'locked_until': '2026-01-04T14:00:00Z'}}`
    -   `{'type': 'NEW_INSIGHT', 'payload': {'focus_score': 78}}`
-   **UI -> Controller (Request):** The UI sends messages to the Controller when the user performs an action.
    -   `{'type': 'SWITCH_MODE_REQUEST', 'payload': {'mode': 'chill'}}`

This unidirectional data flow (state flows down, actions flow up) is a core principle of many modern UI frameworks (like React, Vue, etc.) and helps to keep the application state predictable and easy to debug.

## Technology Choices

The UI can be built with a variety of technologies. The proposed stack is **Electron/Tauri + React**.

-   **Electron / Tauri:** These frameworks allow us to build a cross-platform desktop application using web technologies (HTML, CSS, JavaScript).
    -   **Tauri** is generally preferred as it results in a much smaller and more lightweight application binary compared to Electron.
-   **React:** A powerful and popular library for building user interfaces. Its component-based model and state management features are a perfect fit for this architecture.

By keeping the UI and the Controller as separate processes that communicate over a simple API, we gain several advantages:

-   **Robustness:** If the UI crashes, the Controller (and all its rules) continues to run in the background. The UI can simply be restarted.
-   **Flexibility:** We can completely replace the UI or build alternative UIs (e.g., a simple command-line interface or a mobile app) without touching the core logic of the Controller.
-   **Developer Experience:** A front-end developer can work on the UI without needing to set up a complex Python/Node.js environment, and vice versa.
