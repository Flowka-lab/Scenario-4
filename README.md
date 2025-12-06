 OCR Mail Notification System

Automated AI-powered workflow to scan postal letters, extract the recipient name, match it against a contacts list, and send instant notifications by email (and optionally WhatsApp).

 Overview

This project automates postal mail handling using:

Google Drive → Upload scanned letters

Google Cloud Vision OCR → Extract raw text

OpenAI → Identify and normalize the recipient name

Google Sheets → Log entries + contact directory

Gmail → Notify the recipient with the scanned image

WhatsApp API (optional) → Additional notifications

n8n → Orchestration of the complete workflow

Designed as a simple and maintainable MVP, the system can scale into a full mailroom automation platform.

 Key Features
 OCR & AI Extraction

Extracts text from scanned letters (JPEG, PNG, PDF).

Uses AI to return a clean recipient name only (titles removed, normalized).

Handles uncertain extraction gracefully (returns null if unsure).

📇 Contact Matching

Matches the extracted name with a Normalized column in Google Sheets.

Case-insensitive and accent-insensitive matching.

Supports a simple CRM-style contact directory.

📬 Notifications

If a match is found:

Sends an email containing:

The recipient name

Notification message

The scanned image attached

Optional WhatsApp notification

If no match:

Sheet is updated to NOT_FOUND

No notification is sent

🗂 Logging

Each letter entry includes:

Unique ID

File name

OCR text

Extracted recipient

Match result

Status transitions

Timestamps

Ensures full traceability and auditability.

🧩 Architecture Summary
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
 ┌───────────────┐        ┌──────────────────────┐
 │ Recipient Found│ YES →  │ Send Email (Gmail)   │
 └───────────────┘        └──────────────────────┘
            │ NO
            ↓
   [Update Status: NOT_FOUND]

📁 Repository Structure
/README.md
/GET_STARTED.md
/PROJECT_OVERVIEW.md
/FUNCTIONAL_DESIGN.md
/TECHNICAL_DESIGN.md
/SETUP_GUIDE.md
/CONTRIBUTING_GUIDE.md
/CHANGELOG.md
/FUTURE_ENHANCEMENTS.md
/OCR-UC1-V01.json        → n8n workflow file
/assets/                 → sample letter images

📹 Video Tutorial (Placeholder)

A full walkthrough of the system is available here:
👉 https://youtube.com/placeholder-tutorial

🛠 System Requirements

Google Cloud Project

Vision API enabled

n8n (Cloud or self-hosted)

Gmail Workspace or Gmail API credentials

Google Sheets API access

OpenAI API key (GPT-4.1-mini or equivalent)

Internet access

Recommended load: 1–10 letters/day (MVP), scalable in later versions.

🔐 Accounts to Create
Service	Purpose
Google Drive	Store scanned letters
Google Cloud Vision	OCR text extraction
Google Sheets	Logs + contacts directory
Gmail API	Email notifications
OpenAI	Recipient name extraction
n8n Cloud / self-hosted	Workflow automation
📜 License

Released under the MIT License.

🙌 Contributions

Contributions are welcome!
See CONTRIBUTING_GUIDE.md for guidelines.
