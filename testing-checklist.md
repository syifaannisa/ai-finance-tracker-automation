# Testing Checklist

## Input handling

- [ ] Plain text expense message is parsed correctly.
- [ ] Photo of a receipt is downloaded, base64-encoded, and read correctly by Gemini.
- [ ] PDF document is downloaded, base64-encoded, and read correctly by Gemini.
- [ ] Voice note is downloaded, transcribed by Whisper, and merged into the text pipeline.
- [ ] Unsupported message types are handled without crashing the workflow.

## AI extraction

- [ ] Gemini returns valid, schema-conforming JSON for a well-formed input.
- [ ] Markdown code fences around the JSON response are stripped correctly.
- [ ] Missing fields (merchant, category, item) fall back to safe defaults.
- [ ] A malformed or empty Gemini response triggers the error branch, not a workflow failure.
- [ ] Multiple expense entries in a single message are all captured (not just the first).

## Currency handling

- [ ] Non-USD original amounts are preserved alongside the converted USD amount.
- [ ] USD-denominated inputs pass through without unnecessary conversion errors.

## Google Sheets

- [ ] A successful extraction results in exactly one new row per expense entry.
- [ ] Column values map to the correct columns (see `docs/google-sheets-schema.md`).
- [ ] A Google Sheets write failure surfaces to the user rather than failing silently.

## Telegram feedback

- [ ] A successful entry triggers a confirmation message in the same chat.
- [ ] A failed entry triggers a clear, user-readable error message.
- [ ] The monthly report is sent on schedule and reflects the correct date range.

## Security

- [ ] No real bot token appears in any node URL or Code node.
- [ ] No real spreadsheet identifier is committed.
- [ ] No credential metadata is committed.
- [ ] No real names, phone numbers, or personal expense data appear in sample data or screenshots.
