# Automation-of-Procurement-Reporting-and-Material-Receiving-for-40-SKUs
Developed a system using Google Sheets, Forms, and App Script to automate daily procurement reporting for 40+ SKUs and streamline material receipt tracking for over 1,000 vendor shipments annually. This solution saves 2 hours daily, improves data accuracy, and provides real-time visibility into GRN status, enhancing procurement efficiency.


![image](https://github.com/user-attachments/assets/b2de10be-f126-4e65-b9b5-6209b91e1d12)
![image](https://github.com/user-attachments/assets/2d3fbfa1-78ea-4291-8a77-7e3fad4dd27c)
![image](https://github.com/user-attachments/assets/ced8dc16-2ecb-44df-98c1-b996ec30dc01)


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
```sql
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
```
```sql
function sendDOIWarningEmail() {
  var sheet = SpreadsheetApp.getActiveSpreadsheet().getSheetByName('Nov');
  var data = sheet.getDataRange().getValues();
  
  // Define the HTML table structure for the email
  var emailBody = "<p>Good Morning Sir!</p>";
  emailBody += "<p>The following items have DOI below 15 as per Master Consumble tracker Nov'24:</p>";
  emailBody += "<table border='1' style='border-collapse: collapse;'>";
  
  // Add header row with bold formatting
  emailBody += "<tr style='font-weight: bold;'>";
  emailBody += "<th>Location</th>";
  emailBody += "<th>Article Description</th>";
  emailBody += "<th>DOI(AVERAGE)</th>";
  emailBody += "</tr>";
  
  var emailToSend = false;
  var csvContent = "Location,Article Description,DOI(AVERAGE)\n"; // CSV header
  
  // Loop through the data rows
  for (var i = 1; i < data.length; i++) {
    var doiIndex = data[0].indexOf("DOI(AVERAGE)");
    var locationIndex = data[0].indexOf("Location1");
    var descriptionIndex = data[0].indexOf("Article Description");
    
    var doi = data[i][doiIndex];
    var location = data[i][locationIndex];
    var description = data[i][descriptionIndex];
    
    // Check if DOI is below 15
    if (doi < 15) {
      var roundedDOI = Math.round(doi);

      // Add the row to the email body
      emailBody += "<tr>";
      emailBody += "<td>" + location + "</td>";
      emailBody += "<td>" + description + "</td>";
      // Highlight DOI with red background color in the email body
      emailBody += "<td style='background-color: red;'>" + roundedDOI + "</td>";
      emailBody += "</tr>";
      
      // Add the row to the CSV content
      csvContent += location + "," + description + "," + roundedDOI + "\n";
      
      // Set the DOI cell's background color to red in the sheet
      sheet.getRange(i + 1, doiIndex + 1).setBackground("red");

      emailToSend = true;
    }
  }

  emailBody += "</table>";

  if (emailToSend) {
    // Create a Blob from the CSV content
    var blob = Utilities.newBlob(csvContent, "text/csv", "DOI_Warning_Items.csv");
    
    // Send the email with the CSV file attached
    MailApp.sendEmail({
      to: "guptaraghu386@gmail.com", // Replace with the actual email addresses
      subject: "DOI Warning: Items Below 15 Days",
      htmlBody: emailBody, // Send the email as HTML to preserve table formatting
      attachments: [blob] // Attach the CSV file
    });
  }
}
```



**Daily Reporting**: The script generated daily procurement summaries, sent via email to relevant stakeholders, saving 2 hours per day compared to manual reporting.<br>
**GRN Tracking**: An automated dashboard updated in real-time, showing the status of all GRNs by SKU, vendor, and date, ensuring stakeholders had immediate visibility.<br>
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

