# Google Sheets Schema

The workflow writes each parsed expense as one row with the following columns.

| Column | Type | Description |
|---|---|---|
| `Date` | string (ISO date) | Date the expense occurred, taken from the AI response or the message timestamp |
| `Merchant` | string | Merchant or vendor name extracted by Gemini, or "Unknown merchant" if not detected |
| `Category` | string | Spending category assigned by Gemini (e.g. Food, Transport, Others) |
| `Item` | string | Item or line description, or "-" if not detected |
| `Amount (USD)` | number | Amount converted to USD by Gemini |
| `Original Currency` | string | Currency code of the original transaction |
| `Original Amount` | number | Amount in the original currency |
| `Notes` | string | Any additional notes extracted or added |
| `Timestamp` | string | Row insertion timestamp |

The table above defines the complete Google Sheets schema used by this workflow..
