# GitHub Upload Guide — Upload Kit

## Important Mac note

Files beginning with a dot are hidden by default in Finder:

- `.gitignore`
- `.env.example`
- `.github`

Press:

```text
Command + Shift + .
```

to show or hide hidden files. Do this before dragging any batch folder into GitHub, otherwise `.gitignore`, `.env.example`, and `.github` will silently be left out.

## Repository

Name:

```text
personal-finance-tracker-automation
```

Description:

```text
A multi-input personal expense tracking automation built with n8n, Google Gemini, Groq/Whisper, Telegram, and Google Sheets.
```

Visibility:

```text
Public
```

## Upload sequence

Each numbered folder below is one upload batch. **Upload the contents of each folder to the repository root — do not upload the numbered folder itself.**

### Batch 01 — Documentation foundation

Folder: `01-documentation-foundation`

Upload every item inside it (including hidden files) to the repository root.

Commit message:

```text
docs: initialise project documentation and security policy
```

### Batch 02 — Workflow

Folder: `02-workflow`

Commit message:

```text
feat: add personal finance tracker workflow
```

### Batch 03 — Technical documentation

Folder: `03-technical-documentation`

Commit message:

```text
docs: add architecture, schema, and testing references
```

### Batch 04 — GitHub maintenance

Folder: `04-github-maintenance`

Commit message:

```text
chore: add repository validation and contribution templates
```

## Before each commit

- Confirm files land at the repository root, not nested inside a `0X-...` folder.
- Confirm no API key, bot token, spreadsheet ID, or personal data appears in the diff.
- Confirm folder names remain lowercase.
- Confirm `.gitignore`, `.env.example`, and `.github` are visible and included (Batch 01 and Batch 04).

## After all batches

Add repository topics:

- `n8n`
- `ai-automation`
- `workflow-automation`
- `personal-finance`
- `google-gemini`
- `telegram-bot`
- `whisper-api`

Then pin the repository on your GitHub profile alongside `hotel-ai-concierge-automation`.
