# Gmail to CRM Automation

Automates lead extraction from Gmail and sends structured data to a CRM, reducing manual processing time.

## Overview
This project automates the process of handling incoming leads from email. It scans Gmail threads, extracts key information such as name, email, and phone number, and sends the data to a CRM using webhooks.

I built this during my internship to reduce manual work and make lead processing faster and more efficient.

## Features
- Scans Gmail threads automatically
- Extracts:
  - Email
  - Phone number
  - Name (if available)
- Filters leads from specific sources
- Sends data to a CRM using webhooks
- Labels processed emails to avoid duplicates

## Tech Stack
- JavaScript (Google Apps Script)
- Gmail API
- Webhooks (CRM integration)

## How it works
1. Searches Gmail for unprocessed emails  
2. Extracts lead information using pattern matching  
3. Sends valid leads to the CRM  
4. Marks emails as processed  

## Setup
- Deploy the script in Google Apps Script  
- Configure your webhook URL  
- Run `runOnce()` to process emails  

## Example Output
```json
{
  "firstName": "John",
  "lastName": "Doe",
  "email": "john@email.com",
  "phone": "+1234567890"
}
