# 500: Mode-Specific UI Themes

## A Dynamic Visual Environment

Operion is not just about what you can and cannot do; it's also about how your environment *feels*. To align your digital workspace with your current intention, Operion supports **mode-specific UI themes**.

When you switch modes, Operion can change the visual appearance of your desktop, including:

-   **Color Schemes:** Shifting from a vibrant, colorful theme in Entertainment Mode to a stark, monochrome theme in Work Mode.
-   **Wallpaper:** Automatically changing your desktop wallpaper to match the mood.
-   **UI Elements:** Potentially altering the appearance of window borders, menus, and other system UI elements.

The goal is to use visual cues to reinforce the current mode and make your digital environment a more pleasant and effective space.

## The Psychology of Color and Light

The design of the UI themes is based on the psychological impact of color and light:

-   **Work Mode (Monochrome):** A black-and-white or grayscale color scheme minimizes visual stimulation, reducing the "pull" of distracting UI elements. It creates a sense of seriousness and focus.
-   **Chill Mode (Soft Themes):** Softer, warmer colors (e.g., pastels, earth tones) can create a more relaxed and calming atmosphere.
-   **Entertainment Mode (Vibrant Themes):** Brighter, more saturated colors can enhance the experience of consuming media and playing games.

## Implementation Details

The implementation of UI theming will depend on the underlying operating system.

-   **Changing Wallpapers:** This is a straightforward feature that can be implemented on all major operating systems.
-   **Altering System Colors:** This is more complex.
    -   On some Linux desktop environments, this can be done programmatically.
    -   On Windows and macOS, this might be limited to changing between the system's built-in "light" and "dark" modes.
-   **Custom Theming Engine:** A more advanced implementation could involve a custom theming engine that applies overlays or uses other techniques to control the look and feel of the OS, but this would be a long-term goal.

In the MVP, UI theming may be limited to switching wallpapers and toggling between light and dark mode.
