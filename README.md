# Inventory Management & Automated Alert System

An automated inventory monitoring and email notification system built with **Google Sheets, n8n, Gmail API, and Docker**.

## Live Dashboard

Explore the inventory management system in Google Sheets, including raw materials, lot tracking, stock calculations, automated alerts, and interactive visualizations.

[View Interactive Inventory Dashboard](https://docs.google.com/spreadsheets/d/14km7hxr6Em66WGkihxFUfLWTc4nWNCpidPcmDklfck0/edit?usp=sharing)

## Project Overview

This project demonstrates how workflow automation can support inventory monitoring, improve operational visibility, and reduce manual follow-up tasks.

Designed around a fictional dietary supplement manufacturing environment, the system tracks raw materials, inventory lots, stock movements, and inventory alerts.

## Key Features

- Inventory data organized in Google Sheets
- Raw material and lot tracking
- Monitoring of inventory alerts
- Automated daily workflow execution
- Filtering of pending alerts
- Consolidation of multiple alerts into a single email
- Automatic updates to notification status after successful email delivery
- Prevention of repeated notifications for alerts already marked as sent

## Technologies Used

| Technology | Purpose |
|---|---|
| Google Sheets | Inventory data storage and management |
| n8n | Workflow automation |
| Gmail API | Automated email notifications |
| Docker | Local hosting of n8n |
| JavaScript | Processing alert records |

## Workflow Architecture
![n8n Inventory Automation Workflow](workflow.png)
```text
Schedule Trigger (Daily, 8:00 AM)
          ↓
Google Sheets — Read Alerts
          ↓
Filter — Pending Alerts
          ↓
Aggregate — Consolidate Alerts
          ↓
Gmail — Send Email
          ↓
JavaScript — Process Alert IDs
          ↓
Google Sheets — Mark as Sent
```

## Inventory Structure

The Google Sheets workbook contains five worksheets:

1. **Materials** — Raw material information
2. **Lots** — Inventory lots and expiration dates
3. **Movements** — Inventory transactions
4. **Alerts** — Inventory notifications and their status
5. **Dashboard** — Inventory reporting structure

## Alert Categories

The system is designed to work with inventory alerts such as:

- Expiring Soon
- Low Stock
- Blocked Inventory
- Rejected Inventory

The current n8n workflow processes existing pending alerts from Google Sheets. Automatic detection and generation of new alerts can be added in future versions.

## How It Works

Every day at 8:00 AM, the workflow reads the Alerts worksheet and selects records with a defined alert type and an email status of `Pending`.

The selected records are consolidated into one email notification.

After the Gmail node successfully sends the message, the workflow updates the corresponding records to `Sent`, preventing duplicate notifications.

## Deployment

The automation runs on a self-hosted n8n instance using Docker.

The current deployment is local, so scheduled execution requires the host computer and n8n service to remain running.

The exported workflow is included in this repository with personal information and credentials removed. Users must configure their own Google Sheets and Gmail credentials, spreadsheet references, recipient email address, and timezone.

## Future Improvements

- Automatic alert generation from inventory data
- Configurable stock thresholds
- Automated expiration-date monitoring
- Interactive inventory dashboards
- Cloud deployment for continuous execution

## Project Status

**Functional prototype — portfolio project**

Developed to demonstrate practical skills in workflow automation, data management, API integrations, and JavaScript-based data processing.
