# 300: App Control

## Process Management

Operion uses a proactive polling mechanism to enforce application whitelists/blacklists.

## Enforcement Cycle

Every 3 seconds (configurable), the `Enforcer` task:
1.  Queries the `SystemMonitor` for running applications.
2.  Fetches the current `Mode` policy.
3.  Identifies violating applications.
4.  Instructs the `SystemMonitor` to terminate them.

## Configuration

Policies are defined in `modes.toml` per mode.

-   **Whitelist:** Implicitly blocks all apps *not* in the list (except critical system processes).
-   **Blacklist:** Explicitly blocks apps in the list.

## Critical Process Safety

To prevent system instability, a hardcoded "Safe List" prevents the termination of:
-   `gnome-shell`
-   `Xorg` / `wayland-server`
-   `operiond`
-   `systemd`