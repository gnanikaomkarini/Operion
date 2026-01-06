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

## Implementation on Zorin OS (GNOME)

On the target platform of Zorin OS and other GNOME-based desktops, Operion can achieve deep and comprehensive theme control by programmatically changing the desktop's settings. This is primarily done by issuing commands to the `gsettings` utility from the Rust backend.

This allows for instant, system-wide visual changes that are powerful and feel native to the OS.

### Example `gsettings` Commands:

-   **Changing the GTK (Application) Theme:** To switch to a dark, monochrome theme for Work Mode.
    ```bash
    gsettings set org.gnome.desktop.interface gtk-theme 'Adwaita-dark'
    ```

-   **Changing the Icon Theme:** To switch to a simpler, less distracting icon set.
    ```bash
    gsettings set org.gnome.desktop.interface icon-theme 'elementary'
    ```

-   **Changing the Desktop Wallpaper:** To set a calming background for Chill Mode.
    ```bash
    gsettings set org.gnome.desktop.background picture-uri 'file:///path/to/your/chill-wallpaper.jpg'
    ```

-   **Changing the Shell Theme (Advanced):** Requires the "User Themes" GNOME extension to be installed, but allows changing the theme of the top panel and other shell elements.
    ```bash
    gsettings set org.gnome.shell.extensions.user-theme name 'MyCustomShellTheme'
    ```

By executing these simple commands, the **Operion Controller** can completely reshape the visual environment to match the user's current mode, making the psychological context-switch much more powerful.
