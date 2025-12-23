# GET_STARTED.md

# 🚀 Get Started – OCR Mail Notification System (Scenario 4)

This guide explains how to run the **latest version** of the OCR Mail Notification System using the updated n8n workflow.

---

## 1. What This System Does

- Watches a Google Drive folder for new scanned letters
- Extracts text using Google Cloud Vision OCR
- Uses OpenAI to extract a clean recipient name
- Verifies the recipient against a Google Sheets contact list
- Sends an email notification if a match is found
- Updates logs in Google Sheets
- Moves files automatically:
  - `Letters_Processed` → recipient found
  - `Letters_Unprocessed` → recipient not found

---

## 2. Prerequisites

### Accounts Required
- Google Account
- Google Cloud Project
- n8n (Cloud or self-hosted)
- OpenAI API key
- Gmail account

### Google APIs to Enable
- Vision API
- Google Drive API
- Google Sheets API
- Gmail API

---

## 3. Google Drive Setup

Create three folders:

```
Letters_Inbox
Letters_Processed
Letters_Unprocessed
```

Copy each folder ID (used inside n8n).

---

## 4. Google Sheets Setup

Create one spreadsheet with two tabs.

### letters_inbox
```
Unique_id
gdrive_file_id
gdrive_file_name
ocr_text
extracted_recipient
matched_contact_id
status
created_at
updated_at
```

### contacts
```
Full Name
Normalized
Email
WhatsApp
is_active
```

Normalization rule:
```
UPPERCASE + TRIM + REMOVE ACCENTS
```

---

## 5. Import the n8n Workflow

Import:
```
FlowKa-Lab_Scenario-4.json
```

In n8n:
1. Workflows → Import
2. Upload JSON
3. Save

---

## 6. Configure Credentials

| Node | Credential |
|----|----|
| Google Drive Trigger | Drive OAuth |
| Download File | Drive OAuth |
| Google Vision OCR | Vision API Key |
| Google Sheets | Sheets OAuth |
| Send Email | Gmail OAuth |
| OpenAI Node | OpenAI API Key |

Update:
- Folder IDs
- Spreadsheet ID

---

## 7. Workflow Execution

1. Upload image to `Letters_Inbox`
2. OCR text extracted
3. Recipient name extracted by AI
4. Contact list verified
5. Unified data object created
6. If match:
   - Email sent
   - File moved to `Letters_Processed`
7. If no match:
   - Status updated
   - File moved to `Letters_Unprocessed`

---

## 8. Testing Checklist

- Upload test image
- Verify Google Sheets entry
- Check Gmail inbox
- Confirm file moved correctly

---

## 9. Status Values

| Status | Meaning |
|------|--------|
| NEW | Letter detected |
| Updated | Recipient notified |
| Not Found | No matching contact |

---

## 10. Ready

System is live and operational.
