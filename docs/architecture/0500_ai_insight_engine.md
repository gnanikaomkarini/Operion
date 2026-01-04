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
    4.  The Controller then pushes this text to the UI.

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
