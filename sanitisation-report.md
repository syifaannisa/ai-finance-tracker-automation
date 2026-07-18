# Sanitisation Verification Report

The workflow export was scanned for known-sensitive value patterns before publication.

## Checks performed

- hard-coded Telegram bot tokens (pattern `[0-9]{8,10}:[A-Za-z0-9_-]{30,}`);
- hard-coded Google Gemini / Groq API keys;
- the original personal Google Sheets identifier;
- n8n `credentials` metadata blocks;
- cached Google Sheets result URLs;
- email addresses and phone numbers.

## Findings in the original export

| Finding | Location | Action taken |
|---|---|---|
| Live Telegram bot token hardcoded directly in the URL | 4 HTTP Request nodes (`Get File Path (Image/Document/Voice)`, `Download Audio`) | Replaced with `{{ $env.TELEGRAM_BOT_TOKEN }}` expression |
| Same token hardcoded as a JS string literal | 2 Code nodes (`Build Image URL`, `Build Document URL`) | Replaced with `$env.TELEGRAM_BOT_TOKEN` |
| Real personal Google Sheets ID | `Auto-Save to Spreadsheet` node (`documentId` value + cached result URLs) | Replaced with `YOUR_SPREADSHEET_ID` placeholder, cached URL metadata removed |

No email addresses, phone numbers, or real expense data were found in the workflow export.

## Result

All known sensitive values identified during review have been removed or replaced with placeholders in the published workflow file.

## Important limitation

Automated and manual scanning reduces risk but does not guarantee that every possible sensitive value has been identified. If you fork or adapt this project, re-scan before publishing, and rotate any token or API key that has ever appeared in a shared file — including the token that was found and removed here, which should be treated as compromised and regenerated via BotFather.
