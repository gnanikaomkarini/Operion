# 700: Calendar-Driven Mode Locking

## Integrating Planning with Execution

One of the most powerful features of Operion is its ability to bridge the gap between *planning* your day and *executing* on that plan. It does this by integrating a calendar directly into the system's behavior, a feature known as **Calendar-Driven Mode Locking**.

This feature removes the need for constant self-control by making your pre-committed decisions the default.

## How It Works

The process is designed to integrate with your existing planning workflow, not replace it.

1.  **Export Your Calendar:** You use your existing calendar application (e.g., Google Calendar, or a local app) and export your schedule to a standard file format (e.g., iCalendar `.ics`).
2.  **Point Operion to the File:** In your Operion configuration, you provide the path to this calendar file.
3.  **Assign Modes in Your Calendar:** You can assign a mode to an event by simply putting it in the event title or description (e.g., "Project Report [work]" or "Yoga [chill]"). Operion will parse this.
4.  **Automatic Mode Locking:** When a scheduled time block begins, Operion reads the event from your calendar file, sees the assigned mode, and automatically switches to and **locks** that mode.

## Task-Driven Sessions

To enhance focus, you can link tasks to your scheduled time blocks.

1.  **Simple Task File:** You list your key tasks for the day in a simple text or Markdown file (e.g., `~/tasks.md`).
2.  **Link Tasks to Calendar:** In your calendar event, you can reference a task using a simple tag (e.g., "Finish report #task1").
3.  **Passive Reminder in Panel:** When the scheduled session begins, the text of the Operion panel applet itself can change to display the current task (e.g., "Work: Finish report"). This provides a constant, non-intrusive reminder of your objective without using a floating window or persistent notification.
4.  **Richer Analytics:** This data is used by the `AI Productivity Coach` to provide more meaningful insights, comparing not just how long you worked, but what you accomplished versus what you planned.

## The "Lock"

When a mode is "locked," you cannot easily switch out of it. This creates a powerful commitment device that helps you stick to your plan.

If you try to switch out of a locked mode, Operion will require you to:

1.  **Provide an Explicit Reason:** You will need to type out a reason for why you are breaking your planned session. This simple act of friction is often enough to make you reconsider.
2.  **Wait Out a Cool-Down Timer:** After providing a reason, you may have to wait for a "cool-down" period (e.g., 60 seconds) before the override is complete. This prevents impulsive, in-the-moment decisions from derailing your focus.

The goal of the lock is not to trap you, but to enforce a moment of mindful reflection before you abandon a commitment you made to yourself.

## Calendar Integration

The core of this feature relies on syncing with external calendar services. By reading a standard `.ics` file, Operion can integrate with most calendar providers (Google, Outlook, etc.) without needing complex APIs. The user simply needs to make their calendar available as a local file that Operion can read. This keeps the setup simple and robust.

By linking your schedule directly to your computer's behavior, Calendar-Driven Mode Locking makes it easier than ever to live with intention.
