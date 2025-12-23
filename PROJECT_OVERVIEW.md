# PROJECT_OVERVIEW.md

# 📬 Project Overview – OCR Mail Notification System (Scenario 4)

## 1. Purpose

The OCR Mail Notification System automates the handling of incoming **physical postal letters** by transforming them into **digital events** that can be tracked, routed, and notified automatically.

The system eliminates manual mail sorting by:
- Detecting new scanned letters
- Extracting recipient names using OCR + AI
- Matching recipients against a contact directory
- Sending instant notifications
- Maintaining a clear and auditable mail lifecycle

This version (Scenario 4) introduces **stronger data consolidation** and **explicit file lifecycle management**.

---

## 2. Core Objectives

### Primary Objectives
- Automate detection of incoming scanned letters
- Extract readable text from envelopes or headers
- Reliably identify the intended recipient
- Notify the correct person via email
- Log all actions for traceability
- Ensure no letter is lost or forgotten

### Secondary Objectives
- Keep the system lightweight and low-cost
- Use cloud-native, widely adopted tools
- Enable easy maintenance and future extensions
- Support non-technical operation after setup

---

## 3. What Changed in Scenario 4

Scenario 4 improves operational clarity and robustness.

### Key Enhancements
- **Unified data object** combining OCR, AI extraction, logging, and contact lookup
- **Explicit recipient verification** using active contact flags
- **File lifecycle management** in Google Drive:
  - `Letters_Inbox` → new input
  - `Letters_Processed` → recipient found
  - `Letters_Unprocessed` → recipient not found
- Clear separation between **data processing** and **notification logic**

These changes make the system easier to audit, debug, and scale.

---

## 4. Scope

### In Scope (Current Version)
- Envelope or header scanning (JPG, PNG)
- OCR via Google Cloud Vision
- AI-based recipient name extraction
- Google Sheets used as:
  - Event log
  - Contact directory
- Email notifications via Gmail
- Automatic file movement based on outcome
- Single-letter processing (1 by 1)

### Out of Scope (Current Version)
- Full letter content scanning
- Batch processing
- Database backend
- Admin dashboard
- Authentication or user portals
- Two-way email interaction

---

## 5. Target Users

### Recipients
People who receive notifications when a letter addressed to them arrives.

### Mail Operator
Person or device responsible for scanning and uploading letters.

### System Owner / Operator
Maintains credentials, contact list, and workflow configuration.

---

## 6. High-Level System Components

| Component | Role |
|--------|------|
| Google Drive | Entry point and file lifecycle management |
| Google Vision OCR | Text extraction from images |
| OpenAI | Recipient name extraction |
| Google Sheets | Logging and contact directory |
| Gmail API | Notification delivery |
| n8n | Workflow orchestration |

---

## 7. High-Level Workflow Summary

```
Physical Letter
      ↓
Scan & Upload to Letters_Inbox
      ↓
OCR Text Extraction
      ↓
AI Recipient Identification
      ↓
Contact Verification
      ↓
 ┌─────────────────────────┐
 │ Recipient Found ?        │
 └──────────────┬──────────┘
                │ YES
                ▼
      Send Email Notification
                │
      Move File → Letters_Processed

                │ NO
                ▼
      Update Status
      Move File → Letters_Unprocessed
```

---

## 8. Value Proposition

### Operational Value
- Faster notification of important mail
- Zero manual sorting
- Clear traceability of every letter

### Technical Value
- No custom backend required
- Easy to deploy and maintain
- Modular and extensible workflow

### Business Value
- Professional mail handling experience
- Reduced operational overhead
- Foundation for advanced mailroom automation

---

## 9. Design Philosophy

- **Simplicity first** – MVP before complexity
- **Transparency** – everything logged and visible
- **Deterministic flows** – clear outcomes for every letter
- **Extensibility** – future-ready without overengineering

---

## 10. Summary

The OCR Mail Notification System (Scenario 4) delivers a **clean, reliable, and auditable solution** for handling incoming postal mail using modern cloud and AI services.

It is production-ready for small to medium environments and provides a solid base for future expansion into full mailroom automation platforms.
