# 700: Calendar-Driven Mode Locking

## Integrating Planning with Execution

One of the most powerful features of Operion is its ability to bridge the gap between *planning* your day and *executing* on that plan. It does this by integrating a calendar directly into the system's behavior, a feature known as **Calendar-Driven Mode Locking**.

This feature removes the need for constant self-control by making your pre-committed decisions the default.

## How It Works

The process is simple:

1.  **Plan Your Day:** Operion includes a built-in calendar view. You can create blocks of time for your tasks, just like you would in a normal calendar application.
2.  **Assign Modes to Time Blocks:** For each block of time, you can assign a mode (e.g., "Work," "Chill"). For example, you might schedule a 2-hour "Work Mode" block in the morning for a critical project.
3.  **Automatic Mode Locking:** When a scheduled time block begins, Operion automatically switches to the assigned mode and **locks** it.

## Task-Driven Sessions

To enhance focus and provide clarity, the calendar integration is enhanced with a simple task management system. This allows you to associate a specific intention with each scheduled block of time.

1.  **Simple Task List:** A dedicated area in the Operion UI allows you to list your key tasks for the day (e.g., "Finish Q3 report," "Debug login page").
2.  **Link Tasks to Calendar:** You can drag-and-drop tasks from your list directly onto time blocks in the calendar. A `Work Mode` block now becomes `Work Mode: Finish Q3 report`.
3.  **Passive Reminder:** When the scheduled session begins, the Operion UI will display a constant, non-intrusive reminder of the current task. This helps you quickly regain focus after an interruption.
4.  **Richer Analytics:** This data is used by the `AI Productivity Coach` to provide more meaningful insights, comparing not just how long you worked, but what you accomplished versus what you planned.

## The "Lock"

When a mode is "locked," you cannot easily switch out of it. This creates a powerful commitment device that helps you stick to your plan.

If you try to switch out of a locked mode, Operion will require you to:

1.  **Provide an Explicit Reason:** You will need to type out a reason for why you are breaking your planned session. This simple act of friction is often enough to make you reconsider.
2.  **Wait Out a Cool-Down Timer:** After providing a reason, you may have to wait for a "cool-down" period (e.g., 60 seconds) before the override is complete. This prevents impulsive, in-the-moment decisions from derailing your focus.

The goal of the lock is not to trap you, but to enforce a moment of mindful reflection before you abandon a commitment you made to yourself.

## Calendar Integration

-   **Built-in Calendar:** For the MVP, Operion will feature its own simple, local calendar for planning your days.
-   **External Calendar Sync (Future Goal):** A future version of Operion could sync with external calendar services like Google Calendar or Outlook Calendar. This would allow you to manage your schedule from your preferred application, and have Operion automatically enforce the modes you've planned.

By linking your schedule directly to your computer's behavior, Calendar-Driven Mode Locking makes it easier than ever to live with intention.
