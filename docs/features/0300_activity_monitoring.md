# 400: Activity Monitoring

## Understanding How You Spend Your Time

To provide you with valuable insights and power its more advanced features, Operion needs to understand how you are spending your time on your computer. It does this through a lightweight, local **Activity Monitor** that runs in the background.

The Activity Monitor is designed to be privacy-first. All the data it collects is stored locally on your machine and is never sent to the cloud.

## What Data is Monitored?

The Activity Monitor continuously keeps track of several key data points:

-   **Active Application:** The application that is currently in the foreground.
-   **Foreground Window Title:** The title of the active window (e.g., the name of the document you are editing, the headline of the article you are reading). This is crucial for context.
-   **Time Spent Per Application:** The total amount of time each application is in the foreground.
-   **Idle vs. Active Time:** Operion detects whether you are actively using your computer (e.g., typing, moving the mouse) or if you are idle.
-   **Mode Transitions:** When you switch between modes.

## Privacy First

It is critical to emphasize that this feature is built with privacy as a top priority.

-   **Local Storage:** All activity data is stored in a local SQLite database on your computer. It does not leave your machine.
-   **No Keystroke Logging:** Operion does **not** log your keystrokes. It only records which application is active, not what you type into it.
-   **No Screen Capture:** Operion does **not** take screenshots of your screen.
-   **Data Processing:** All data processing and analysis happens locally on your device.

## How This Data is Used

The data collected by the Activity Monitor is the foundation for many of Operion's most powerful features:

-   **Insights & Analytics:** It powers the daily and weekly reports on your focus and productivity.
-   **AI-Powered Content Awareness:** The window titles are used to classify the content you are consuming.
-   **Smart Mode Transitions:** The system can learn from your activity to suggest or automatically switch modes.
-   **AI Productivity Coach:** The data provides the basis for the personalized suggestions you receive.

You will have control over the Activity Monitor and can pause or disable it if you choose, though this will limit the functionality of other features.
