# 0500: The AI Insight Engine

## From Raw Data to Actionable Insights

The **AI Insight Engine** is the component responsible for the "smart" features of Operion, such as Content Awareness and the AI Productivity Coach. Its role is to take the raw data collected by the **System Hooks & Monitors** and transform it into higher-level, actionable insights.

This engine is designed as a modular service that the **Operion Controller** can communicate with. This separation ensures that the core logic of the Controller remains simple and focused, while the complex and potentially resource-intensive AI tasks are handled by a dedicated component.

## A Service-Oriented Approach

The AI Engine can be thought of as an internal microservice. The Controller communicates with it via a simple API.

### Example Interactions:

-   **Content Classification:**
    1.  The Controller receives a `window_title_changed` event from a Monitor.
    2.  It sends the window title (e.g., "Python Tutorial for Beginners") to the AI Engine's `/classify` endpoint.
    3.  The AI Engine returns a classification: `{'category': 'educational', 'topic': 'programming'}`.
    4.  The Controller uses this classification to update the focus score.

-   **Productivity Coach Summary:**
    1.  At the end of the day, the Controller gathers all the relevant data (time in modes, distractions, etc.).
    2.  It sends this data to the AI Engine's `/generate_summary` endpoint.
    3.  The AI Engine formats the data into a prompt, sends it to an LLM, and returns the generated text to the Controller.
    4.  The Controller then displays this text in a native desktop notification.

## Pluggable AI Models

A key aspect of this design is that the AI Engine itself is a thin wrapper around different **AI providers** or **models**. This allows the user to choose which AI they want to use, balancing privacy, cost, and performance.

The engine will have an interface for an `AIProvider`, and we can create concrete implementations for different services.

### `AIProvider` Interface (Conceptual):

```python
class AIProvider:
    """An interface for a generic AI model provider."""

    def classify_content(self, text: str) -> dict:
        """Classifies a piece of text into predefined categories."""
        pass

    def generate_text(self, prompt: str) -> str:
        """Generates text based on a given prompt."""
        pass
```

### Pluggable Implementations:

-   `GeminiProvider`: An implementation that uses the Google Gemini API. This would provide high-quality results but requires an internet connection and sends data to the cloud.
-   `OpenAIProvider`: An implementation that uses the OpenAI (GPT) API.
-   `LocalLLMProvider`: An implementation that runs a local large language model (e.g., via Ollama or llama.cpp). This would be the most private option but would require a more powerful machine and might have lower accuracy.
-   `SimpleClassifierProvider`: A non-LLM, local provider that uses simpler, traditional machine learning models (or even just keyword matching) for basic classification. This would be very private and lightweight.

The user can select which provider they want to use in the configuration file, and the AI Insight Engine will load the corresponding module. This makes the AI component of Operion highly modular and user-configurable.

## Recommended Ollama Models

Choosing the right local LLM is a critical balance between performance, capability, and hardware requirements. While Operion allows any Ollama model to be used, the following recommendations are based on the specific needs of the AI Insight Engine.

The AI's two primary tasks have competing needs:
-   **Real-time Content Classification:** Requires a **fast** response to avoid delaying user interactions (like blurring a webpage).
-   **AI Coach Summary Generation:** Requires a **high-quality, creative** model to generate insightful and human-like text.

### Model Comparison

| Model | Est. RAM | Primary Use Case | AI Coach Quality | Classification Speed | Hardware Requirement |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **`phi-3:mini`** | ~4GB | Speed-critical tasks | Basic to Good | Fastest | Low (runs well on most modern laptops) |
| **`mistral:7b`** | ~8GB | General purpose | Good | Fast | Medium (requires decent RAM) |
| **`llama3:8b`** | ~8GB | Quality-critical tasks | Excellent | Fast | Medium-High (requires decent RAM, GPU recommended) |
| **`gemma:7b`** | ~8GB | General purpose | Good | Fast | Medium (requires decent RAM) |

---

### Head-to-Head: `llama3:8b` vs. `phi-3:mini`

The choice for the best *default* model comes down to a direct trade-off between the two best-in-class options:

-   If we prioritize the **quality of the AI Productivity Coach**, `llama3:8b` is the clear winner. Its ability to understand context, follow instructions, and generate creative text will provide a significantly better user experience for the end-of-day summary. The trade-off is a slightly higher resource footprint and potentially a few hundred milliseconds more latency on classification tasks.

-   If we prioritize **raw speed and minimal resource usage**, `phi-3:mini` is the champion. It will be near-instantaneous for content classification, ensuring the most responsive experience possible. The trade-off is that the AI Coach summaries may be more simplistic and less insightful.

---

### Final Recommendation

For the initial release, the recommended default model is **`llama3:8b`**.

**Reasoning:** The small amount of extra latency for classification is a worthy trade-off for the dramatic increase in quality for the AI Productivity Coach, which is a major user-facing feature. The 8B parameter size is the modern "sweet spot" for powerful local AI on consumer hardware.

However, **`phi-3:mini`** will be documented as the official "lightweight alternative" for users on lower-spec machines or for those who prefer maximum responsiveness above all else. The final choice will always remain in the user's hands via the configuration file.

### Pre-installed Model Considerations: `llava:7b`

If you already have `llava:7b` installed, it is a perfectly viable and recommended option to start with.

-   **Capability:** As a 7-billion parameter language model, `llava:7b` is capable of handling both the real-time content classification and the AI Coach summary generation effectively. Its text-processing capabilities are strong.
-   **Multimodal Aspect:** While `llava:7b` is a multimodal model (understanding both text and images), Operion will primarily utilize its text-processing features for the current implementation, as the browser extension approach does not require image analysis. The multimodal aspect does not negatively impact its performance for our use case.
-   **Comparison:** It offers similar performance for classification as `mistral:7b` or `gemma:7b`. For AI Coach summaries, it provides good quality, though `llama3:8b` might offer slightly more nuanced text generation if that becomes a priority.
