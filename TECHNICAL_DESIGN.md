# TECHNICAL_DESIGN.md

#  Technical Design – OCR Mail Notification System

## 1. Architecture Overview

The system is event-driven and orchestrated entirely by n8n.

```
Google Drive
   ↓
n8n Trigger
   ↓
OCR (Vision API)
   ↓
OpenAI Extraction
   ↓
Sheets Log + Contact Check
   ↓
Decision
   ↓
Email + File Move
```

---

## 2. Key Components

| Component | Description |
|---------|------------|
| Google Drive | Input + lifecycle management |
| Google Vision | OCR text extraction |
| OpenAI | Recipient name extraction |
| Google Sheets | Logs + contacts |
| Gmail API | Notifications |
| n8n | Orchestration |

---

## 3. Data Model

### letters_inbox
- Unique_id
- gdrive_file_id
- gdrive_file_name
- ocr_text
- extracted_recipient
- matched_contact_id
- status
- created_at
- updated_at

### contacts
- Full Name
- Normalized
- Email
- WhatsApp
- is_active

---

## 4. Unified Data Object (Scenario 4)

A single object is built mid-workflow containing:
- OCR text
- Extracted name
- Contact match
- Status
- File IDs

This reduces branching complexity.

---

## 5. APIs Used

- Google Vision: `DOCUMENT_TEXT_DETECTION`
- OpenAI: Chat Completions (JSON output)
- Google Sheets: append/update
- Gmail: send email
- Google Drive: move file

---

## 6. Error Handling

| Error | Action |
|-----|-------|
| OCR failure | Mark failed |
| AI failure | Mark failed |
| Email failure | Retry / log |
