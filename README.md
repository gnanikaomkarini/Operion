# Operion 🧠⚙️  
**An Intent-Aware Operating System Layer for Focused Living**

Operion is a mode-driven, intelligent operating system *experience* that adapts your digital environment based on **intent, time, and behavior**.

Instead of treating all apps and activities equally, Operion introduces system-wide **modes** that reshape your UI, control app access, and guide user behavior using AI-powered insights — helping you work deeply, rest intentionally, and consume entertainment mindfully.

Operion is built as a lightweight operating layer on top of an existing OS (Linux / Windows / macOS), making it practical, extensible, and user-centric.

---

## ✨ Why Operion?

Modern operating systems optimize for performance — not humans.

Operion optimizes for:
- Focus without friction
- Intentional mode switching
- Behavioral awareness
- Sustainable productivity

> Operion doesn’t ask for discipline.  
> It designs the system around it.

---

## 🧠 Core Concept: Modes

Operion introduces **system-wide modes** that define *how* and *why* your computer behaves at any moment.

### 🧑‍💻 Work Mode
- Distraction-free environment
- Only work-related apps accessible
- Minimal, monochrome UI
- Notifications suppressed
- Time-locked sessions

### 😌 Chill Mode
- Light productivity and recovery
- Softer UI themes
- Music and reading-friendly setup
- Reduced restrictions

### 🎬 Entertainment Mode
- Intentional leisure
- Media-centric UI
- No productivity tracking penalties
- Guilt-free consumption

Modes affect:
- App visibility & launch permissions
- UI themes and layouts
- Notification behavior
- System policies

---

## 🔒 App Control & Restrictions

Operion enforces focus using **policy-based app access**:

- Whitelist / blacklist apps per mode
- Hide or block distracting apps
- Restrict specific websites or domains
- Progressive enforcement:
  - Warnings → UI dimming → temporary lock

Example:
```text
Work Mode:
✔ VS Code
✔ Terminal
✔ Docs
✖ YouTube
✖ Instagram
✖ Games
⏱️ Activity Monitoring
```
Operion continuously monitors system activity to understand how time is spent:

- Active applications
- Foreground window titles
- Time spent per app
- Idle vs active time
- Mode transitions

All activity data is stored locally and processed privately.

## 🎥 AI-Powered Content Awareness
Operion uses AI to classify content — not just apps.

For example, when using YouTube:

- Reads video title and metadata
- Classifies content as:
  - Educational
  - Entertainment
  - Low-value distraction

This enables:

- Accurate focus scoring
- Context-aware restrictions
- Meaningful insights

## 📊 Insights & Analytics
Operion provides actionable insights instead of raw stats.

**Daily Insights**
- Focus score
- Deep work duration
- Distraction percentage
- Mode usage breakdown

**Weekly Insights**
- Productivity trends
- Peak focus hours
- Common distraction patterns
- Suggested schedule improvements

Example:

“Your focus drops most often between 3–4 PM. Consider scheduling lighter tasks during this window.”

## 🗓️ Calendar-Driven Mode Locking
Operion integrates planning directly into system behavior.

- Plan your day on a built-in calendar
- Assign modes to time blocks
- Automatically lock modes during scheduled intervals

Override requires:
- Explicit reason
- Cool-down timer

This removes the need for constant self-control.

## 🔁 Smart Mode Transitions (Advanced)
Operion can optionally switch modes automatically based on behavior:

- Sustained coding → Work Mode
- Media apps detected → Entertainment Mode
- Idle + music → Chill Mode

Manual control always remains available.

## 🧠 AI Productivity Coach
At the end of each day, Operion generates a reflective summary:

- Planned vs actual work time
- Focus consistency
- Distraction sources
- Personalized suggestions

Example:

“You planned 5 hours of deep work and completed 3.8 hours. Morning sessions showed higher focus.”

## 🛠️ Architecture Overview
```text
+---------------------------+
|        Operion UI         |
|  (Mode Switch, Dashboard) |
+---------------------------+
            |
+---------------------------+
|     Operion Controller    |
| (Rules, Policies, Modes)  |
+---------------------------+
            |
+---------------------------+
|   System Hooks & Monitors |
| (Apps, Windows, Activity) |
+---------------------------+
            |
+---------------------------+
|     AI Insight Engine     |
| (Classification & Advice) |
+---------------------------+
```

## 🧪 MVP Scope
**Phase 1 (MVP):**

- Manual mode switching
- App blocking per mode
- Activity tracking
- Mode-specific UI themes
- Daily insights
- Calendar-based mode locking

**Phase 2 (Advanced):**

- Auto mode switching
- AI content classification
- Productivity coach
- Mental fatigue detection
