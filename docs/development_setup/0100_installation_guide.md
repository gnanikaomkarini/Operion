# 0100: Installation Guide

This guide provides the step-by-step instructions to set up your development environment for building Operion on **Linux**. Follow these steps in order.

---

## 1. Rust Language Toolchain

Rust is the core language of the project. We will install it using `rustup`, the official Rust toolchain installer.

1.  **Install `rustup`:**
    -   Open your terminal and run the following command. It will download and run the official installation script.
    -   `curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh`
2.  **Follow On-Screen Instructions:**
    -   The script will prompt you to choose an installation type. The default option (`1) Proceed with installation (default)`) is recommended.
3.  **Configure your Shell:**
    -   After installation, the script will tell you to configure your current shell. Run the command it provides, which is typically:
    -   `source "$HOME/.cargo/env"`
4.  **Verify Installation:**
    -   Close and reopen your terminal, then run:
    -   `rustc --version`
    -   You should see the version of the Rust compiler, e.g., `rustc 1.78.0 ...`.

---

## 2. Node.js and pnpm

Node.js is a required dependency for Tauri's web-based frontend. We will use `pnpm` as our JavaScript package manager because it's fast and efficient.

1.  **Install Node.js:**
    -   It is recommended to install Node.js through a version manager like `nvm` or `fnm`. However, for simplicity, you can download the LTS version directly from the [official Node.js website](https://nodejs.org/).
2.  **Verify Node.js Installation:**
    -   In a new terminal, run:
    -   `node --version` and `npm --version`
    -   You should see versions for both.
3.  **Install `pnpm`:**
    -   We will use `npm` (which comes with Node.js) to install `pnpm` globally.
    -   `npm install -g pnpm`
4.  **Verify `pnpm` Installation:**
    -   `pnpm --version`

---

## 3. OS-Specific Prerequisites for Tauri (Linux)

Tauri relies on system-level build tools and libraries to create native applications. On Linux, you need to install the following:

-   `build-essential` (for compilers and development tools)
-   `curl`, `wget`, `file` (common utilities)
-   `libssl-dev` (OpenSSL development libraries)
-   `libgtk-3-dev`, `libayatana-appindicator3-dev`, `librsvg2-dev` (GTK+3 libraries and dependencies for UI)
-   `webkit2gtk-4.1` (Tauri uses WebView2, which often relies on WebKitGTK for Linux)

On Debian-based systems (like Ubuntu), run:

```bash
sudo apt update
sudo apt install build-essential curl wget file libssl-dev libgtk-3-dev libayatana-appindicator3-dev librsvg2-dev webkit2gtk-4.1
```
For other Linux distributions (Fedora, Arch, etc.), you'll need to adapt these packages to your distribution's package manager. Refer to the [Tauri Prerequisites documentation](https://tauri.app/v1/guides/getting-started/prerequisites) for more details.

---

## 4. Ollama (for Local AI)

Ollama allows you to run powerful open-source language models locally.

1.  **Download Ollama:**
    -   Go to the [Ollama website](https://ollama.com/).
    -   Download and run the installer for your operating system (ensure you select the Linux installer).
2.  **Pull a Model:**
    -   After installation, you need to download a model. We recommend starting with a small, fast model like `phi3`.
    -   Open your terminal and run:
    -   `ollama pull phi3`
3.  **Run the Ollama Server:**
    -   The Ollama application runs a server in the background automatically. To verify it's working, you can list the models you have downloaded:
    -   `ollama list`
    -   You should see `phi3` in the output.

Your development environment is now fully configured and ready for building Operion.
