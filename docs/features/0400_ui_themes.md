# 500: UI Themes

## Implementation

Operion manages the desktop's visual state via the **GSettings** API. This allows for native, system-wide theme transitions without custom rendering engines.

## GSettings Integration

The controller executes state changes using the `org.gnome.desktop` schemas.

### Theme Switching
Changes the application theme (GTK4/Libadwaita).

-   **Command:** `gsettings set org.gnome.desktop.interface gtk-theme 'THEME_NAME'`
-   **Constraint:** The theme must be installed in `~/.themes` or `/usr/share/themes`.

### Wallpaper Switching
Changes the desktop background.

-   **Command:** `gsettings set org.gnome.desktop.background picture-uri 'FILE_URI'`
-   **Dark Mode Support:** Modern GNOME also requires setting `picture-uri-dark`.

## Shell Theme (Optional)
If the user has the "User Themes" extension installed, Operion can also switch the shell theme (top bar, overview).

-   **Schema:** `org.gnome.shell.extensions.user-theme`
-   **Key:** `name`