# SETUP_GUIDE.md

# ⚙️ Setup Guide – Scenario 4

## 1. Prerequisites
- Google Cloud Project
- n8n instance
- OpenAI API key

---

## 2. Enable Google APIs
- Vision API
- Drive API
- Sheets API
- Gmail API

---

## 3. Drive Setup
Create folders:
- Letters_Inbox
- Letters_Processed
- Letters_Unprocessed

---

## 4. Sheets Setup
Create spreadsheet with:
- letters_inbox
- contacts

---

## 5. n8n Setup
1. Import `FlowKa-Lab_Scenario-4.json`
2. Configure credentials
3. Update folder & sheet IDs
4. Activate workflow

---

## 6. Test
Upload an image to `Letters_Inbox` and verify flow.
