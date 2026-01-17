# Development Setup

## Prerequisites

### System Dependencies (Debian/Ubuntu/Pop!_OS)
Operion targets GNOME-based Linux distributions.

```bash
sudo apt update
sudo apt install -y \
    build-essential \
    libssl-dev \
    pkg-config \
    libglib2.0-dev \
    libgtk-4-dev \  # Required for the Journaling UI binary
    libdbus-1-dev \
    sqlite3 \
    libsqlite3-dev
```

### Rust Toolchain
Operion requires the latest stable Rust toolchain.

**Minimum Supported Rust Version (MSRV):** 1.75.0

```bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
rustup update stable
```

### AI Model (Ollama)
For AI features, install Ollama and pull the default model.

```bash
curl -fsSL https://ollama.com/install.sh | sh
ollama pull llama3
```

## Build Instructions

Operion consists of multiple binaries.

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/yourusername/operion.git
    cd operion
    ```

2.  **Build the project (Workspace):**
    This will build the daemon, native host, and UI components.
    ```bash
    cargo build --release
    ```
    *Output binaries in `target/release/`:*
    *   `operiond` (The core daemon)
    *   `operion-native` (Browser native messaging host)
    *   `operion-journal` (GTK4 Journaling UI)

3.  **Run tests:**
    ```bash
    cargo test
    ```

## Project Structure

-   `src/bin/operiond.rs`: Entry point for the daemon.
-   `src/bin/operion-native.rs`: Entry point for browser host.
-   `src/bin/operion-journal.rs`: Entry point for the UI.
-   `src/controller/`: Core logic and state management.
-   `src/monitors/`: OS-specific hooks (GNOME implementation).
-   `src/storage/`: SQLite interactions.

```