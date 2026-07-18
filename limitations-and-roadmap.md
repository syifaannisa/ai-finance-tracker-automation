# Limitations and Roadmap

## Current limitations

- **Single-user design.** The workflow assumes one Telegram chat is the only source of expenses; it does not separate data by user or household.
- **No duplicate detection.** The same receipt sent twice will be logged twice.
- **No budget awareness.** The workflow logs and reports spending but does not compare it against a budget or send threshold alerts.
- **Whisper language hint is fixed.** The `Voice-to-Text Engine` node is currently configured for Indonesian (`language: "id"`); other languages need a manual change.
- **No retry logic on AI failures.** If Gemini or Groq returns an error, the user gets a clear error message in Telegram, but the workflow does not automatically retry the request.
- **Currency conversion accuracy depends on the AI model.** Gemini estimates the USD conversion at extraction time rather than calling a live exchange-rate API, so amounts may drift from the actual rate on the transaction date.

## Roadmap

- Add a live exchange-rate lookup instead of relying on Gemini's estimated conversion.
- Add duplicate-receipt detection (e.g. hashing the image before processing).
- Add configurable budget thresholds with proactive Telegram alerts.
- Add a category-level breakdown chart to the monthly report.
- Support multiple Telegram chats/users writing to separate sheet tabs or a `user_id` column.

## Portfolio scope note

This project is a personal-use demonstration built to show multi-modal input handling and AI-based structured extraction in n8n. It is not positioned as a production-ready financial application, and it does not implement bank-grade security, audit logging, or multi-user access control.
