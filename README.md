# Automation-of-Procurement-Reporting-and-Material-Receiving-for-40-SKUs
Developed a system using Google Sheets, Forms, and App Script to automate daily procurement reporting for 40+ SKUs and streamline material receipt tracking for over 1,000 vendor shipments annually. This solution saves 2 hours daily, improves data accuracy, and provides real-time visibility into GRN status, enhancing procurement efficiency.

# Introduction
In procurement operations, tracking and managing incoming shipments from multiple vendors is crucial for inventory accuracy and process efficiency. Delays in reporting, errors in data entry, and difficulty in accessing real-time data were common bottlenecks. To streamline these processes, I developed a solution using Google Sheets, Forms, and App Script, which automated daily reporting, improved material receipt accuracy, and enabled real-time tracking of Goods Receipt Notes (GRN).

# Problem Statement
Our procurement team handles 40+ SKUs with over 1,000 vendor shipments each year. Manual entry and processing of shipment and receipt data were:

**Time-consuming**: Manual reporting took 2-3 hours daily.
**Error-prone**: Frequent data entry errors affected tracking accuracy.
**Lacking Real-time Data**: No immediate insight into shipment status, leading to potential delays in restocking or shipment scheduling.
These challenges highlighted the need for a more efficient, automated approach to manage procurement reporting and GRN tracking.

# Solution
The goal was to automate the daily procurement reporting process, optimize material receiving, and create a GRN tracker to enable real-time visibility. Here’s a step-by-step breakdown of how the project was implemented:

# Data Collection with Google Forms:

A google form was created for warehouse teams to confirm receipt details, including discrepancies (if any) and condition on arrival.
Data Integration with Google Sheets:
Responses from Google Forms automatically populated Google Sheets.
A master tracking sheet compiled vendor shipment data,DOI(Days of inventory for packaging material) received goods details, and any discrepancies or issues noted upon delivery.

# Automation with Google App Script:

# DOI Warning Email Automation Script

This Google Apps Script automates the process of identifying items with a Days of Inventory (DOI) below 15, sending an email notification, and attaching a CSV file with details. It highlights the DOI values in red for quick reference.

## Features
- Generates an HTML email with a table listing items below the DOI threshold.
- Highlights DOI values in red within the email and in the Google Sheet.
- Attaches a CSV file with the low DOI items.

## Setup Instructions
1. Add this script to your Google Sheets project.
2. Configure the recipient's email in the `MailApp.sendEmail` function.
3. Set up a trigger to automate the script execution as needed.

## Usage
- Open the script in your Google Sheets project and run `sendDOIWarningEmail()` manually or schedule it to run daily.

---

### License
This project is licensed under the MIT License.






**Daily Reporting**: The script generated daily procurement summaries, sent via email to relevant stakeholders, saving 2 hours per day compared to manual reporting.
**GRN Tracking**: An automated dashboard updated in real-time, showing the status of all GRNs by SKU, vendor, and date, ensuring stakeholders had immediate visibility.
**Notifications**:
Automated alerts informed the procurement team and warehouse managers of discrepancies or delays in shipments, allowing for quicker resolutions.

# Technology Used
**Google Sheets:** For storing, tracking, and reporting procurement data.
**Google Forms:** For data collection from vendors and warehouse teams.
**Google App Script:** To automate data processing, report generation, and real-time tracking of GRNs.

# Real-Time Example
A vendor ships a batch of SKU A100 to the warehouse. They log the shipment details via the Google Form, which automatically populates Google Sheets. When the shipment arrives, the warehouse team logs receipt data through another form, noting any discrepancies (e.g., damaged goods, incorrect quantity). The App Script checks for discrepancies, and sends notifications if there’s a mismatch, ensuring both teams are immediately informed.

# Challenges Faced
**Data Consistency:** Ensuring that data from vendors and warehouse teams matched consistently was challenging.

**Solution:** Implemented validations in Google Forms to minimize errors during data entry and set up automated checks with App Script.
**Integration Delays:** Google Sheets occasionally lagged with large data volumes from multiple forms.

**Solution:** Optimized the App Script to run batch processes during low-traffic periods.

# Conclusion
The automation of the procurement reporting process and the real-time GRN tracker have streamlined daily operations, saved 2 hours per day, improved data accuracy, and enabled real-time visibility for stakeholders. This solution has also set a foundation for potential future integrations, such as advanced analytics or ERP systems.

