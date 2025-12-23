# OCR Mail Notification System

Automated AI-powered workflow to scan postal letters, extract the recipient name, match it with a contacts list, and send notifications by email (and optionally WhatsApp).

## Overview

This project automates the handling of postal mail using:

- Google Drive for uploading scanned letters
- Google Cloud Vision OCR for raw text extraction
- OpenAI for identifying and normalizing the recipient name
- Google Sheets for logging and contact directory
- Gmail for sending notification emails with attachments
- Optional WhatsApp API for additional notifications
- n8n for workflow orchestration

The system is built as a simple and maintainable MVP, with the ability to scale into a full mailroom automation platform.

## Key Features

### OCR and AI Extraction
- Extracts text from scanned JPEG, PNG, or PDF documents.
- Uses AI to return a clean, normalized recipient name only.
- Handles uncertainty by returning `null` if no reliable name is detected.

### Contact Matching
- Matches the extracted name against a `Normalized` column in Google Sheets.
- Case-insensitive and accent-insensitive matching.
- Supports a basic CRM-like contact directory.

### Notifications

- Processed letters are automatically moved into Letters_Processed or Letters_Unprocessed folders in Google Drive to ensure a clean file lifecycle

**When a match is found:**
- Sends an email including:
  - The identified recipient name
  - A notification message
  - The scanned image attached
- Optional WhatsApp notification

**When no match is found:**
- Sheet is updated with `NOT_FOUND` status
- No notification is sent

### Logging

Each letter entry is logged with:
- Unique ID
- File name
- OCR text
- Extracted recipient
- Matching result
- Status transitions
- Timestamps

## Architecture Summary


```
[Google Drive Folder Trigger]
            ↓
     [Download Image]
            ↓
     [Google Vision OCR]
            ↓
 [OpenAI Recipient Extractor]
            ↓
[Google Sheets – Letters Log]
            ↓
[Google Sheets – Contacts Lookup]
            ↓
   ┌─────────────────┐         ┌──────────────────────┐
   │ Recipient Found │  YES →  │   Send Email (Gmail) │
   └─────────────────┘         └──────────────────────┘
            │ NO
            ↓
   [Update Status: NOT_FOUND]
```

## Repository Structure

```
/README.md
/GET_STARTED.md
/PROJECT_OVERVIEW.md
/FUNCTIONAL_DESIGN.md
/TECHNICAL_DESIGN.md
/SETUP_GUIDE.md
/CONTRIBUTING_GUIDE.md
/CHANGELOG.md
/FUTURE_ENHANCEMENTS.md
/OCR-UC1-V01.json        → n8n workflow
/assets/                 → sample letter images
```

## Video Tutorial

A full walkthrough of the workflow is available at:
https://youtube.com/placeholder-tutorial

## System Requirements

- Google Cloud Project
- Google Vision API enabled
- n8n (self-hosted or cloud)
- Gmail Workspace or Gmail API credentials
- Google Sheets API access
- OpenAI API key (GPT-4.1-mini or similar)
- Internet connection

Recommended usage: 1–10 letters per day for the MVP; scalable in future releases.

## Accounts to Create

| Service | Purpose |
|---------|---------|
| Google Drive | Store scanned letters |
| Google Cloud Vision | OCR text extraction |
| Google Sheets | Logging + contacts directory |
| Gmail API | Email notifications |
| OpenAI | Recipient extraction |
| n8n Cloud or self-hosted | Workflow automation |

## License

This project is distributed under the MIT License.

## Contributions

Contributions are welcome.
See `CONTRIBUTING_GUIDE.md` for more details.
