# 0700: Configuration and Modularity in Practice

## Tying It All Together

This document summarizes how Operion's architectural principles of **modularity** and **user-centric configuration** work in practice. The goal is to create a system that is both powerful out-of-the-box and endlessly adaptable to individual workflows.

Operion is not designed to be a rigid system. It is a framework for you to define *your own* rules for a focused life.

## How Users Can Customize Operion

Customization is not an afterthought; it's the core of the experience. Here are the primary ways a user can tailor Operion to their needs, without writing any code.

### 1. Defining Modes and Rules

As shown in the `Operion Controller` document, the most powerful customization happens in the `modes.yaml` configuration file.

**Your Scenario: Allowing Spotify in Work Mode**

You mentioned that for you, Spotify is a productivity tool. The default Operion setup might block it in Work Mode. To change this, you would simply open `~/.config/operion/modes.yaml` and edit it:

```yaml
# Default configuration might look like this:
modes:
  work:
    name: "Work Mode"
    policy: "whitelist"
    list:
      - "Code"
      - "Terminal"

# You would change it to this:
modes:
  work:
    name: "Work Mode"
    policy: "whitelist"
    list:
      - "Code"
      - "Terminal"
      - "Spotify" # Simply add it to the list!
```
The **Operion Controller** will automatically detect this change and, from that moment on, Spotify will be allowed to run during your work sessions. You can do this for any application or website, crafting a digital environment that is perfectly suited to you.

### 2. Choosing an AI Provider

In the `config.yaml` file, you can choose your AI provider.

-   If you value **privacy** above all else, you can switch to the `local` provider.
-   If you want the **highest quality** insights and have an API key, you can use `gemini` or `openai`.

```yaml
ai:
  provider: "local" # Changed from "gemini"
```

## How Developers Can Extend Operion

The modular, interface-driven design makes it possible for developers to extend Operion's functionality.

### 1. Adding Support for a New OS

If a developer wants to make Operion work on a new Linux desktop environment (e.g., Sway), they don't need to understand the core application logic. They only need to:

1.  Create a new class, `SwaySystemMonitor`.
2.  Implement the methods defined in the `SystemMonitor` interface (e.g., `get_active_window_info`, `block_app`) using Sway's specific tools (like `swaymsg`).
3.  Add the logic to the main application loader to detect and load `SwaySystemMonitor` when running on Sway.

### 2. Adding a New AI Provider

If a new, open-source AI model is released, a developer can integrate it into Operion by:

1.  Creating a new class, `NewAIModelProvider`.
2.  Implementing the methods from the `AIProvider` interface (`classify_content`, `generate_text`).
3.  Adding the provider to the list of available providers in the AI Insight Engine.

This modularity is the key to Operion's long-term vision. It allows the core team to focus on the stability and performance of the Controller, while empowering the community to build integrations and extensions that make the system more powerful and accessible for everyone.
