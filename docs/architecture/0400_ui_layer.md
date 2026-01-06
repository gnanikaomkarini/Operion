# 0400: Desktop Integration & UI

## "Headless" by Design

The core philosophy of Operion has shifted to favor deep OS integration over a traditional application model. Operion is "headless"—it runs as a background service and does not have a primary application window. The user should feel that Operion is a *native feature* of their desktop, not a separate app they need to open and manage.

The UI is not a single entity but a collection of interaction points that integrate directly into the user's desktop environment, initially targeting **Zorin OS (GNOME)**.

## Primary Interaction Points

The user interacts with Operion through the native elements of their desktop:

1.  **System Panel Applet:** The main entry point is a simple icon in the Zorin/GNOME top panel. Clicking this icon reveals a menu to view the current mode and manually switch to another. This is the primary point of control.
2.  **Native Notifications:** The system communicates with the user via the desktop's native notification system. This is used for AI Coach summaries, suggesting a mode switch, or warning about a blocked website.
3.  **Configuration Files:** As before, the deep customization of modes and rules happens by editing human-readable `.yaml` or `.toml` files.

## Decoupling the UI from the Core Logic

The architectural principle of keeping the "UI" and the "core logic" separate remains, but the implementation is different. The **Operion Controller** (the Rust background service) remains the "brain." It contains all the state and business logic.

The UI components (panel applet, notifications) are "dumb" clients that react to commands or state changes from the Controller.

### Communication Channel

Instead of IPC with a web view, the Controller communicates directly with the Desktop Environment's services:

-   **Controller -> Desktop (Commands):** The Controller issues commands to change the desktop environment.
    -   To change the GTK theme, it will execute a `gsettings` command.
    -   To post a notification, it will use a D-Bus library to send a message to the GNOME notification service.
-   **Desktop -> Controller (Events):** The panel applet, when clicked, sends a signal to the Controller (e.g., via D-Bus or a local socket) to request a mode switch.

## Technology Choices

The technology stack for the UI is now based on direct interaction with the host OS.

-   **Rust:** The core Controller remains in Rust.
-   **D-Bus:** For robust, native communication with the GNOME desktop environment and its various services (notifications, system tray), a Rust D-Bus library like `zbus` is the ideal choice.
-   **Shell Commands:** For simple, fire-and-forget actions like changing a theme or wallpaper, the Controller can directly execute shell commands (e.g., `gsettings set org.gnome.desktop.interface gtk-theme 'Adwaita-dark'`).

By using the desktop's own tools, we ensure that Operion feels completely native and respects the user's environment. This approach is more robust and resource-efficient than running a separate, web-based UI. A web-based dashboard could be added later as an optional, secondary interface for detailed analytics, but it is not the primary method of interaction.