# Changelog

## [1.0.0] - 2026-07-16

### Added

- Multi-input Telegram expense capture workflow (text, photo, document, voice).
- Google Gemini-based structured expense extraction.
- Groq/Whisper voice transcription branch.
- Scheduled monthly reporting workflow.
- Architecture, setup, and configuration documentation.
- Secure environment-variable configuration example.
- Sanitised public workflow export.

### Security

- Removed a hardcoded Telegram bot token from four HTTP Request nodes and two Code nodes.
- Removed a real personal Google Sheets identifier from the Google Sheets append node.
