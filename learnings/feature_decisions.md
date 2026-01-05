# Feature Decision Log

This document records the reasoning behind key feature decisions made for the Operion project. The goal is to provide context for future development and to understand the trade-offs that were considered.

---

## 1. Intelligent Browser Protection

### Decision
The feature will be implemented using a **companion browser extension** rather than by taking screenshots of the user's screen. The setup will use a **guided installation** process from within the main app.

### Reasoning
The initial idea was to "see the screen" and analyze its content. A direct screenshot-and-analyze approach was considered.

However, we chose the browser extension path for two critical reasons:

1.  **Privacy & User Trust:** Even with a local AI model (like Ollama), the act of constantly taking screenshots is highly invasive and could erode user trust. A browser extension is more privacy-respecting because it can access the text and structure (DOM) of a webpage without needing to "see" the pixels on the screen. It adheres to the **Principle of Least Privilege**.
2.  **Performance:** Analyzing image data from screenshots is thousands of times more resource-intensive (CPU, GPU, RAM) than parsing simple text from a webpage's DOM. The screenshot method would have caused significant system slowdown and battery drain, making the application impractical for many users.

The "guided installation" was decided upon because browsers explicitly prevent external applications from silently installing extensions for security reasons. Our chosen method (detecting browsers, opening the correct store page automatically) provides the most seamless and secure setup possible under these constraints.

---

## 2. Proactive Nudges & Warnings

### Decision
This feature idea was **rejected and discarded**.

### Reasoning
The user provided crucial feedback that a system which frequently sends notifications and suggestions (e.g., "You've been on this site for 15 minutes") would ultimately feel **nagging and distracting**.

This clarified a core design principle for Operion: it should be a **strong, silent partner** that shapes the user's environment, not a vocal coach that interrupts them. The goal is to reduce cognitive load, not add to it with a new stream of notifications to process.

---

## 3. Journaling Integration

### Decision
This feature will be implemented as a **"Session Review"** that appears *after* a user switches out of `Work Mode`, not as a "Daily Kick-off" prompt.

### Reasoning
The initial idea was to prompt the user at the start of the day. The user refined this, pointing out that a prompt at the end of a work session would be more valuable for reflection and less intrusive. This shifts the feature's purpose from "planning" (which is better handled by the new Task-Driven Sessions feature) to "reflection," which provides better context for the AI coach and aligns with the goal of mindful productivity.

---

## 4. Task-Driven Work Sessions

### Decision
A simple to-do list will be integrated with the calendar, allowing specific tasks to be linked to `Work Mode` blocks. A passive reminder of the current task will be displayed in the UI.

### Reasoning
This feature was developed directly from the rejection of "Proactive Nudges." Instead of the system "nagging" the user, this feature empowers the user to define their own intentions. It provides a non-intrusive, passive reminder of the user's *own stated goal*, helping them re-focus after an interruption without adding a new source of distraction. It turns the system into a silent tool for accountability to oneself.

---

## 5. Feature Organization: "Stretch Goals"

### Decision
A `stretch_goals` directory was created to house features that are visionary but not core to the initial product.

### Reasoning
The user correctly identified that certain proposed features, like **Physical Environment (IoT) Integration** and **Focus Pacts (Social Accountability)**, depend on external factors (user hardware, network effects) and are not essential for the MVP. Separating these into a "stretch goals" category helps to keep the core project scope manageable while preserving valuable long-term ideas.

---

## 6. Ollama Model Selection - Evaluation of `llava:7b`

### Decision
While `llama3:8b` is the recommended default, `llava:7b` was deemed a perfectly viable and recommended model, especially if already installed by the user.

### Reasoning
Upon user inquiry, it was confirmed that the pre-installed `llava:7b` model is suitable for Operion's AI tasks. As a 7-billion parameter language model, its text-processing capabilities are sufficient for:
-   **Real-time Content Classification:** It can quickly and accurately classify text content from web pages.
-   **AI Coach Summary Generation:** It can generate good quality summaries, comparable to other 7B models.

Although `llava:7b` is a multimodal (vision-capable) model, this aspect is not utilized by Operion's current browser-extension-based implementation. Its multimodal nature does not impede its performance for our use case. Using an already installed model streamlines the user's setup and reduces the initial barrier to entry, aligning with Operion's user-centric philosophy.
