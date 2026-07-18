# Security Policy

## Public repository policy

This repository must not contain:

- Telegram bot tokens;
- Google Gemini or Groq API keys;
- OAuth client secrets or n8n credential metadata;
- personal Google Sheets identifiers;
- production webhook URLs;
- real names, email addresses, phone numbers, or chat identifiers;
- real expense records.

All secrets should be stored in n8n credentials, environment variables, or an appropriate secrets manager — never inside the exported workflow JSON.

## What was found and fixed before publishing

The original workflow export contained a live Telegram bot token hardcoded in six places (four HTTP Request node URLs and two Code nodes), and a real personal Google Sheets ID hardcoded in the Google Sheets "append" node. Both were replaced with environment-variable references / placeholder values. See [`sanitisation-report.md`](sanitisation-report.md) for details.

**If you are reusing this project with your own bot token:** treat any token that has ever appeared in a shared file, screenshot, or chat history as compromised, and regenerate it via [@BotFather](https://t.me/BotFather) before use.

## Before publishing changes

1. Export a clean workflow copy from n8n.
2. Remove credential metadata and production identifiers (spreadsheet IDs, bot tokens, cached result URLs).
3. Replace sensitive values with environment-variable references.
4. Scan the repository for secrets (token patterns, emails, phone numbers).
5. Review any screenshots or sample data for personal information.

## Reporting a security issue

Please do not open a public issue containing sensitive information. Contact the repository owner privately through the professional contact method listed on their portfolio.
