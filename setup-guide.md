# Setup Guide

## Prerequisites

- A running n8n instance (self-hosted or n8n Cloud).
- A Telegram account.
- A Google account with access to Google Sheets.
- A free [Groq](https://console.groq.com) API key (for Whisper transcription).
- A [Google AI Studio](https://aistudio.google.com) API key (for Gemini).

## 1. Create a Telegram bot

1. Message [@BotFather](https://t.me/BotFather) on Telegram.
2. Run `/newbot` and follow the prompts.
3. Copy the bot token BotFather gives you.
4. Set it as an environment variable on your n8n instance: `TELEGRAM_BOT_TOKEN=<your-token>` (see [`.env.example`](../.env.example)).

## 2. Import the workflow

1. In n8n, choose **Import from File** and select `workflows/personal-finance-tracker.json`.
2. n8n will show every node that previously had a credential attached, now unbound. This is expected — credentials are never included in an export.

## 3. Re-bind credentials

Re-attach your own credentials to the following nodes:

| Node | Credential type needed |
|---|---|
| `Telegram Trigger`, `Telegram: Success Confirmation`, `Telegram: Error Message`, `Telegram: Send Report` | Telegram API credential (your bot token) |
| `Voice-to-Text Engine` | Generic Header Auth credential (`Authorization: Bearer <your Groq API key>`) |
| `AI Receipt Reader` | Generic Query Auth credential (`key=<your Gemini API key>`) |
| `Read Sheets Data`, `Auto-Save to Spreadsheet` | Google Sheets OAuth2 credential |

Note: the four `Get File Path (...)` / `Download Audio` HTTP Request nodes call the public Telegram Bot API directly and read the bot token from `{{ $env.TELEGRAM_BOT_TOKEN }}` rather than from a credential — make sure that environment variable is set on your n8n instance (Step 1).

## 4. Create the Google Sheet

1. Create a new Google Sheet with a tab matching the schema in [`google-sheets-schema.md`](google-sheets-schema.md).
2. Open the `Read Sheets Data` and `Auto-Save to Spreadsheet` nodes and pick your sheet from the document selector (this replaces the `YOUR_SPREADSHEET_ID` placeholder automatically).

## 5. Test each input type

1. Send a plain text message describing an expense, e.g. "Coffee at Starbucks, 65000 IDR".
2. Send a photo of a receipt.
3. Send a PDF invoice as a document.
4. Send a voice note describing a purchase.

Each should result in a confirmation message in Telegram and a new row in the sheet.

## 6. Enable the monthly report

Activate the workflow so the `Monthly Report Schedule` trigger runs on its configured interval. Adjust the schedule's cron expression to match how often you want to receive a summary.
