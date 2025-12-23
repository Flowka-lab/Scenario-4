# FUNCTIONAL_DESIGN.md

#  Functional Design – OCR Mail Notification System 

## 1. Purpose
This document describes **what the system does**, from a business and user perspective, aligned with the updated Scenario 4 n8n workflow.

---

## 2. Core Use Cases

### UC1 – Process a New Incoming Letter
**Trigger:** A scanned letter image is uploaded to `Letters_Inbox`.

**Flow:**
1. Detect new file in Google Drive
2. Extract text via OCR
3. Extract recipient via AI
4. Log letter in Google Sheets
5. Verify recipient in contacts list
6. Decide outcome
7. Move file to correct folder

---

### UC2 – Notify Recipient
**Condition:** Recipient found and active.

**Result:**
- Send email notification
- Update letter status
- Archive file in `Letters_Processed`

---

### UC3 – Handle Unmatched Letter
**Condition:** No matching recipient.

**Result:**
- Update status to `Not Found`
- Move file to `Letters_Unprocessed`

---

## 3. User Stories

- As a **recipient**, I want to be notified instantly when mail arrives.
- As an **operator**, I want mail handled automatically without sorting.
- As a **system owner**, I want traceability for every letter.

---

## 4. Workflow Logic (Functional)

```
Upload Letter
   ↓
OCR Extraction
   ↓
AI Name Parsing
   ↓
Contact Verification
   ↓
Found? ── YES → Notify + Archive
   │
   NO
   ↓
Mark Not Found + Archive
```

---

## 5. Functional Requirements

- Must process letters one-by-one
- Must support JPG/PNG
- Must normalize names before matching
- Must log every letter
- Must move files based on outcome
- Must not notify inactive contacts

---

## 6. Status Lifecycle

| Status | Meaning |
|------|--------|
| NEW | Letter detected |
| Updated | Recipient notified |
| Not Found | No match |

---

## 7. Non-Goals
- Batch processing
- Full letter scanning
- User authentication
