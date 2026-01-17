# 1100: Browser Protection

## Architecture

This feature requires a **Native Messaging Host** architecture.

1.  **Browser Extension:** A WebExtension (Manifest v3) installed in Chrome/Firefox.
2.  **Native Host:** A Rust binary (`operion-native`) registered with the browser.
3.  **Controller:** The main daemon.

## Communication Flow

1.  **Extension** observes navigation event.
2.  **Extension** sends URL/Title to `operion-native` via Stdio.
3.  **Native Host** forwards request to **Controller** (via IPC/Unix Socket).
4.  **Controller** checks Policy/AI.
5.  **Controller** returns `Action::Block` or `Action::Allow`.
6.  **Extension** applies CSS Blur if `Action::Block`.

## Security

The Native Host validates that the caller is the whitelisted Extension ID.