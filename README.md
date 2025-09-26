## Overview

Nathan's Workflow is an automated n8n workflow that processes weekly ERP orders, filters and transforms data, stores records in Airtable, calculates booking statistics, and sends a summary notification to Discord. The workflow is triggered every Monday at 9 AM and integrates multiple services for seamless data flow and reporting.



## Program Structure

### Nodes

1. **Schedule Trigger**  
   Initiates the workflow every week (Monday, 9 AM).

2. **HTTP Request**  
   Fetches order data from a custom ERP webhook using header authentication.

3. **If**  
   Checks if the order status is `"processing"`.

4. **Edit Fields (Set)**  
   Extracts and sets `orderID` and `employeeName` from the incoming data.

5. **AirTable**  
   Creates a new record in the "orders" table of the specified Airtable base.

6. **Code**  
   Calculates booking statistics (`totalBooked`, `bookedSum`).

7. **Discord**  
   Sends a summary message to Discord with booking stats and the unique ID.

---

## Workflow Diagram

![Workflow Screenshot](./workflow-screenshot.png)

*Place your screenshot image as `workflow-screenshot.png` in the same directory as this README.*

---

## Usage Instructions

### Prerequisites

- n8n installed and running
- Credentials for:
  - ERP webhook (HTTP header authentication)
  - Airtable (Personal Access Token)
  - Discord (Webhook URL)

### Setup Steps

1. **Import the Workflow**
   - Download `Nathan's workflow.json`.
   - In n8n, go to "Workflows" > "Import" and select the JSON file.

2. **Configure Credentials**
   - Set up HTTP Request node with your ERP webhook URL and authentication.
   - Add your Airtable Personal Access Token in the AirTable node.
   - Add your Discord Webhook URL in the Discord node.

3. **Customize Fields (Optional)**
   - Adjust field mappings in the Edit Fields and AirTable nodes as needed.
   - Modify the Discord message content if desired.

4. **Activate the Workflow**
   - Enable the workflow in n8n.
   - The workflow will run automatically every Monday at 9 AM.

5. **Monitor Results**
   - Check Discord for weekly booking summaries.
   - Review Airtable for stored order records.

---

## License

This workflow is intended for internal automation and integration purposes.

