# 🧾 Invoice Parser Agent — n8n

> Gmail receives invoice PDF → Groq AI extracts all data → logs to Google Sheets → Telegram notification. Zero manual data entry.

![n8n](https://img.shields.io/badge/n8n-workflow-FF6B6B?style=flat-square)
![Groq](https://img.shields.io/badge/Groq-LLaMA%203.3%2070B-F55036?style=flat-square)
![Gmail](https://img.shields.io/badge/Gmail-API-EA4335?style=flat-square&logo=gmail&logoColor=white)
![Google Sheets](https://img.shields.io/badge/Google%20Sheets-logging-34A853?style=flat-square&logo=google-sheets)
![License](https://img.shields.io/badge/license-MIT-green?style=flat-square)

## ✨ What it does

When an invoice arrives in Gmail, the agent:
1. **Detects** new email with PDF attachment
2. **Extracts** PDF content and sends to Groq AI
3. **Parses** amount, date, vendor, invoice number, VAT
4. **Logs** structured row to Google Sheets
5. **Notifies** accountant via Telegram with summary

## 🏗️ Architecture

```
Gmail (new invoice email)
        │
        ▼
┌───────────────┐
│  Gmail Trigger │  detects PDF attachment
└──────┬────────┘
       │
       ▼
┌───────────────┐
│   Groq AI      │  extracts: vendor, amount,
│ LLaMA 3.3 70B  │  date, invoice_no, VAT, currency
└──────┬────────┘
       │
       ▼
┌───────────────┐
│  Code (JS)     │  parses JSON, formats row
└──────┬────────┘
       │
       ▼
┌───────────────┐
│ Google Sheets  │  appends invoice record
└──────┬────────┘
       │
       ▼
┌───────────────┐
│   Telegram     │  notifies accountant
└───────────────┘
```

## 📋 Google Sheets Output

| Date | Vendor | Invoice No | Amount | VAT | Currency | Status |
|------|--------|------------|--------|-----|----------|--------|
| 2025-06-03 | ACME Sp. z o.o. | FV/2025/123 | 4500.00 | 23% | PLN | parsed ✅ |

## 🚀 Setup

1. n8n → **Import from file** → select `workflow.json`
2. Add credentials: Gmail OAuth2, Groq API key, Google Sheets OAuth2, Telegram Bot token
3. Replace `YOUR_GOOGLE_SHEET_ID` with your Sheet ID
4. Toggle workflow **Active**

## 🛠️ Tech Stack

| Component | Technology |
|-----------|-----------|
| Automation | n8n |
| AI Model | Groq — LLaMA 3.3 70B |
| Email | Gmail API |
| Storage | Google Sheets |
| Notifications | Telegram Bot API |

---
*Built by [VinteliVision](https://vintelivision.com) — AI automation for Polish SMBs.*
