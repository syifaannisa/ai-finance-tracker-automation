# Architecture

## Overview

The workflow has two independent entry points sharing one Google Sheet as the data layer:

1. **Expense capture** — triggered by an incoming Telegram message (text, photo, document, or voice).
2. **Monthly reporting** — triggered on a recurring schedule, independent of user activity.

## Expense capture flow

```
Telegram Trigger
      │
      ▼
Input Type Router (switch: text / photo / document / voice)
      │
      ├── text ─────────────► Prepare Text Input
      │
      ├── photo ────────────► Get File Path (Image) ─► Build Image URL (download + base64)
      │
      ├── document ─────────► Get File Path (Document) ─► Build Document URL (download + base64)
      │
      └── voice ────────────► Get File Path (Voice) ─► Download Audio ─► Voice-to-Text Engine (Groq Whisper)
                                                                              │
                                                                              ▼
                                                                    Prepare Transcribed Text
      │
      ▼ (all branches)
Merge All Inputs
      │
      ▼
Build Gemini Prompt
      │
      ▼
AI Receipt Reader (Google Gemini 2.5 Flash)
      │
      ▼
Parse AI Response  (defensive JSON parsing)
      │
      ▼
Success? (IF node)
      │
      ├── true ──► Auto-Save to Spreadsheet ──► Telegram: Success Confirmation
      │
      └── false ─► Telegram: Error Message
```

## Monthly reporting flow

```
Monthly Report Schedule (Schedule Trigger)
      │
      ▼
Read Sheets Data (Google Sheets: getAll)
      │
      ▼
Calculate Monthly Report (Code node: aggregation)
      │
      ▼
Telegram: Send Report
```

## Key design decisions

- **Single workflow instead of a multi-workflow split.** Unlike the [Hotel AI Concierge](../hotel-ai-concierge-automation) project, all input channels here converge on the same review surface (one Telegram chat, one spreadsheet), so a single linear workflow was simpler to build, test, and maintain than splitting by input type.
- **Two AI providers, not one.** Gemini handles structured multimodal extraction (text + image + document), while Groq's hosted Whisper model is used specifically for audio transcription, since Gemini's audio handling was not part of this workflow's original design.
- **Defensive parsing around the AI response.** Gemini occasionally wraps JSON in markdown code fences or fails outright; the `Parse AI Response` node strips fences, wraps parsing in try/catch, and always returns a `success` flag with a user-facing message so the Telegram reply never fails silently.
- **Currency normalisation at extraction time.** The prompt asks Gemini to return both the original amount/currency and a USD-converted amount, so the spreadsheet stays comparable across currencies without a separate conversion step.
