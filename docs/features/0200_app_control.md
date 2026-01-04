# 300: App Control & Restrictions

## Policy-Based App Access

A key feature of Operion is its ability to enforce focus by controlling access to applications and websites based on the current mode. This is achieved through a flexible, policy-based system that you can configure to match your needs.

The goal is not to be a rigid taskmaster, but to gently guide you towards your intentions. When you are in "Work Mode," Operion helps you stay there by making it harder to access distractions.

## Whitelists and Blacklists

For each mode, you can define a "whitelist" or a "blacklist" of applications.

-   **Whitelist:** Only the applications on this list are allowed to run. All other applications are blocked. This is the recommended approach for "Work Mode," as it's easier to define what you *need* to work than to list everything that *might* distract you.
-   **Blacklist:** The applications on this list are blocked. All other applications are allowed. This is useful for "Chill Mode," where you might want to block only the most demanding work applications.

### Example Configuration for Work Mode:

-   **Whitelist:**
    -   `VS Code`
    -   `Terminal`
    -   `Google Docs` (as a web app)
    -   `Slack`
-   **Blocked (Implicitly):**
    -   `YouTube`
    -   `Instagram`
    -   `Steam` (and all other games)

## Website and Domain Restrictions

In addition to desktop applications, Operion can also restrict access to specific websites and domains. This is crucial, as many modern distractions are web-based.

You can add specific URLs (e.g., `youtube.com`, `facebook.com`) to the blacklist for each mode. When you try to access a blocked site, Operion will prevent the page from loading.

## Progressive Enforcement

Operion understands that sometimes a hard block is not the best approach. It can use a "progressive enforcement" system to gently nudge you back on track.

1.  **Warning:** The first time you try to access a blocked app or site, Operion might show a simple warning: "You are in Work Mode. Are you sure you want to proceed?"
2.  **UI Dimming:** If you continue to try to access the distraction, Operion could dim the screen of the distracting application, making it visually unappealing.
3.  **Temporary Lock:** As a last resort, Operion can temporarily lock you out of the distracting application or even the entire system for a short period (e.g., 5 minutes).

This multi-stage approach gives you an opportunity to correct your course without feeling punished.

## Implementation Notes

-   Application blocking will be implemented using OS-specific APIs to identify and close or hide application windows.
-   Website blocking will likely be implemented via a local proxy or by editing the system's `hosts` file.
