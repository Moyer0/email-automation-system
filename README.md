# Gmail to CRM Automation

This project automates the process of extracting leads from Gmail and sending them to a CRM system using webhooks.

## Overview
I built this script to reduce manual work when handling incoming leads. It scans emails, extracts key information like name, email, and phone number, and automatically sends the data to a CRM.

## Features
- Scans Gmail threads automatically
- Extracts:
  - Email
  - Phone number
  - Name (if available)
- Filters leads (only processes emails from specific sources like homes.com)
- Sends data to CRM using webhook
- Labels processed emails to avoid duplicates

## Tech Stack
- JavaScript (Google Apps Script)
- Gmail API
- Webhooks (CRM integration)

## How it works
1. Searches Gmail for unprocessed emails  
2. Extracts lead information using regex  
3. Sends valid leads to CRM  
4. Marks emails as processed  

## Why I built this
During my web development internship, I worked on automating lead processing to improve efficiency and reduce manual data entry.

## What I learned
- Working with APIs and webhooks  
- Automating workflows  
- Data extraction using regex  
- Handling real-world edge cases  

## Note
Sensitive information such as API URLs has been partially hidden for security.

## Author
Eduardo Moyer  
Computer Science student at UTEP
