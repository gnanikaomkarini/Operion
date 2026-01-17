# Roadmap

## Core MVP (Phase 1)
- **System-Wide Modes:** Implementation of `Work`, `Chill`, `Entertainment` modes with configuration support (`modes.yaml`).
- **App Control:** Whitelist/Blacklist enforcement via OS process monitoring.
- **UI Themes:** Integration with GNOME `gsettings` for theme/wallpaper switching.
- **Activity Monitoring:** Local SQLite storage of window titles and focus duration.
- **Basic Analytics:** Daily summaries via local notification.

## Advanced Features (Phase 2)
- **Smart Mode Transitions:** Heuristic-based automatic mode switching (e.g., "Idle + Music" -> Chill Mode).
- **Mental Fatigue Detection:** Local anomaly detection model to identify decreased interaction speed or increased error rates.
- **AI Productivity Coach:** LLM-based end-of-day summaries using local models (e.g., Ollama/Llama3).

## Long-Term Research (Phase 3)
- **Physical Environment Integration:** IoT integration (Philips Hue, Sonos) to sync room lighting/audio with system mode.
- **Focus Pacts:** Opt-in, privacy-preserving social accountability features sharing focus status.
- **Mode-Specific Soundscapes:** Audio stream/file playback triggering on mode entry.
