# Project Overview

## Personal Finance Tracker Automation

A multi-input personal expense tracker built with n8n, Google Gemini, Groq (Whisper), Telegram, and Google Sheets.

## Business problem

Manually logging day-to-day expenses is easy to abandon, especially when spending happens in different formats: a quick cash purchase, a photographed receipt, an emailed invoice, or a verbal note said in passing.

## Solution

A single Telegram bot accepts four input types — text, photo, document, and voice — and normalises all of them through one AI extraction pipeline into a shared Google Sheet, with a scheduled report sent back to the user.

### Implemented functionality

- Multi-modal input routing (text / photo / document / voice)
- Voice transcription via Groq's hosted Whisper endpoint
- AI-based structured extraction via Google Gemini (merchant, category, item, currency, USD conversion)
- Defensive JSON parsing with user-facing error handling
- Automatic Google Sheets logging
- Scheduled monthly report delivered via Telegram

### Planned improvements

- Budget threshold alerts
- Category-level monthly breakdown chart
- Multi-user support (currently single-chat)

## What this project demonstrates

- handling multiple heterogeneous input types in a single automation;
- integrating two different AI providers (Gemini for extraction, Groq/Whisper for transcription);
- prompt design for schema-constrained JSON output;
- defensive error handling around AI responses;
- scheduled reporting workflows;
- secure public configuration using environment variables and credential re-binding;
- technical documentation and handover thinking.

## Important scope note

This is a personal-use portfolio project. The original Telegram bot token and Google Sheet ID used during development have been rotated/removed and replaced with placeholders in this published version.
