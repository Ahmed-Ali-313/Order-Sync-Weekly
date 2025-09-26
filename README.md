## Overview

Nathan's Workflow is an automated n8n workflow designed to process weekly ERP orders, filter and transform data, store records in Airtable, calculate booking statistics, and send a summary notification to Discord. The workflow is triggered every Monday at 9 AM and integrates multiple services for seamless data flow and reporting.

---

## Program Structure

### Nodes

1. **Schedule Trigger**
   - **Purpose:** Initiates the workflow every week (Monday, 9 AM).
   - **Type:** `n8n-nodes-base.scheduleTrigger`

2. **HTTP Request**
   - **Purpose:** Fetches order data from a custom ERP webhook.
   - **Authentication:** HTTP Header with a unique ID.
   - **Type:** `n8n-nodes-base.httpRequest`

3. **If**
   - **Purpose:** Checks if the order status is `"processing"`.
   - **Type:** `n8n-nodes-base.if`

4. **Edit Fields (Set)**
   - **Purpose:** Extracts and sets `orderID` and `employeeName` from the incoming data.
   - **Type:** `n8n-nodes-base.set`

5. **AirTable**
   - **Purpose:** Creates a new record in the "orders" table of the specified Airtable base.
   - **Fields:** `orderID`, `employeeName`, `Attachments`, `Attachment Summary`
   - **Type:** `n8n-nodes-base.airtable`

6. **Code**
   - **Purpose:** Calculates booking statistics:
     - `totalBooked`: Number of booked orders.
     - `bookedSum`: Total value of booked orders.
   - **Type:** `n8n-nodes-base.code`

7. **Discord**
   - **Purpose:** Sends a summary message to Discord with booking stats and the unique ID.
   - **Type:** `n8n-nodes-base.discord`

---

## Workflow Logic

1. **Trigger:** The workflow starts with the Schedule Trigger node.
2. **Fetch Data:** The HTTP Request node retrieves order data from the ERP system.
3. **Filter:** The If node checks if the order status is `"processing"`.
4. **Transform:** If true, the Edit Fields node extracts relevant fields.
5. **Store:** The AirTable node creates a new record in Airtable.
6. **Calculate:** The Code node computes booking statistics.
7. **Notify:** The Discord node sends a summary message to a Discord channel.

---

## Connections

- **Schedule Trigger → HTTP Request**
- **HTTP Request → If**
- **If → Edit Fields → AirTable**
- **If → Code → Discord**

---

## Credentials

- **HTTP Request:** Uses header authentication (`unique_id`).
- **AirTable:** Uses a personal access token.
- **Discord:** Uses a webhook account.

---

## Customization

- **Schedule:** Adjust the trigger time as needed.
- **Endpoints:** Change the ERP webhook URL or Airtable base/table.
- **Fields:** Map additional fields in Airtable if required.
- **Discord Message:** Customize the notification content.

---

## Usage

1. **Configure Credentials:** Set up authentication for HTTP Request, Airtable, and Discord nodes.
2. **Deploy Workflow:** Activate the workflow in n8n.
3. **Monitor:** Check Discord for weekly booking summaries and Airtable for stored records.

---

## License

This workflow is intended for internal automation and integration purposes.
