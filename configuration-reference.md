# Configuration Reference

## Environment variables

| Variable | Used by | Description |
|---|---|---|
| `TELEGRAM_BOT_TOKEN` | `Get File Path (Image)`, `Get File Path (Document)`, `Get File Path (Voice)`, `Download Audio`, `Build Image URL`, `Build Document URL` | Your Telegram bot token from BotFather. Used directly in Telegram Bot API file-download URLs. |

## n8n credentials

| Credential | Type | Used by |
|---|---|---|
| Telegram API | `telegramApi` | `Telegram Trigger`, `Telegram: Success Confirmation`, `Telegram: Error Message`, `Telegram: Send Report` |
| Groq Header Auth | Generic — Header Auth (`Authorization: Bearer <key>`) | `Voice-to-Text Engine` |
| Gemini Query Auth | Generic — Query Auth (`key=<key>`) | `AI Receipt Reader` |
| Google Sheets OAuth2 | `googleSheetsOAuth2Api` | `Read Sheets Data`, `Auto-Save to Spreadsheet` |

## Google Sheet

The spreadsheet ID is picked directly through the node's document selector in n8n once you re-bind the Google Sheets credential — it is not stored as an environment variable in this workflow. Set it in both `Read Sheets Data` and `Auto-Save to Spreadsheet`.

## AI model configuration

| Setting | Value |
|---|---|
| Gemini model | `gemini-2.5-flash` |
| Whisper model (via Groq) | `whisper-large-v3` |
| Whisper language hint | `id` (Indonesian) — change in the `Voice-to-Text Engine` node's body parameters if you speak a different language |
