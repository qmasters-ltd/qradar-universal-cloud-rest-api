# Cisco Umbrella DNS Logs API Connector for QRadar

Integrate **Cisco Umbrella DNS logs** directly into **IBM QRadar** using the Universal Cloud REST API protocol. This guide explains how to generate your API credentials, configure QRadar, map required parameters, and understand the connector’s data collection workflow.

---

## 1. How to Generate Cisco Umbrella API Credentials

1. **Log in** to the [Cisco Umbrella Dashboard](https://dashboard.umbrella.com).
2. Navigate to **Admin** → **API Keys** (or **Integrations** > **API Keys**, depending on your UI version).
3. Click **Create API Key** or **New API Key**.
4. Enter a clear label for the key, then click **Generate**.
5. **Copy and securely store** your `Client ID` and `Client Secret`. *(They will not be displayed again.)*
6. Make sure the key has permissions for **DNS Activity Reports** via the Umbrella Reporting API.

---

## 2. QRadar Log Source Configuration

You will use a **Workflow XML** to configure the Universal Cloud REST API protocol in QRadar for collecting Umbrella DNS logs.

### Steps

1. **Log in** to QRadar and go to the **Admin** panel.
2. Open the **DSM Editor** app and click **Create New**.
   - Name: `Cisco Umbrella DNS Logs`
3. In the **Admin** panel, open the **QRadar Log Source Management** app.
4. Click **New Log Source** → **Single Log Source**.
5. On the **Select a Log Source Type** page, choose **Cisco Umbrella DNS**.
6. On the **Select Protocol Type** page, select **Universal Cloud REST API**.
7. On the **Configure the Log Source Parameters** page:
    - Enter a **log source name** (e.g., `Cisco Umbrella DNS Logs`).
    - Click **Configure Protocol Parameters**.
8. On the **Configure the Protocol Parameters** page:
    - Enter a log source identifier (e.g., `CiscoUmbrellaDNS`).
    - **Paste the Workflow XML** into the **Workflow** field.
    - **Paste the Workflow Parameters XML** (see below) into the **Workflow Parameters Values** field.
    - **Important:** *Turn off* "Coalescing Events" to avoid grouping events by Source and Destination IP.
9. Click **Test Protocol Parameters** and then **Start Test**.
10. If any errors occur, adjust the parameters and retest.
11. Click **Finish** when successful.

---

## 3. Cisco Umbrella Workflow Parameters Mapping

> **Note:**  
> Cisco Umbrella DNS logs are often **high volume** and can significantly increase your QRadar Events Per Second (EPS) rate.  
> 
> **Recommendation:**  
> To reduce the risk of API throttling, missed logs, or QRadar processing errors, set the polling **interval to 1 minute**. This helps ensure logs are collected in manageable batches, maintaining data integrity and system performance.


Below are the supported parameters.  
**Bold fields are required.**

| Parameter                   | Name                    | Default Value       | Type            | Required | Description                                                                            |
|-----------------------------|-------------------------|---------------------|-----------------|----------|----------------------------------------------------------------------------------------|
| **api_host**                | API Host URL            | `https://api.umbrella.com` | String     | True     | Cisco Umbrella API base URL.                                                           |
| **client_id**               | Client ID               | N/A                 | Authentication  | True     | Cisco Umbrella API Client ID.                                                          |
| **client_secret**           | Client Secret           | N/A                 | Authentication  | True     | Cisco Umbrella API Client Secret.                                                      |
| max_results                 | Max Results per Poll    | 5000                | Integer         | False    | Maximum number of DNS events to retrieve per poll.                                     |
| initial_event_fetch_period  | Initial Fetch Period    | 1                   | Integer (hours) | False    | How many hours back to fetch events on first collection (default: 1 hour).             |
| **identifier**              | Log Source Identifier   | CiscoUmbrellaDNS    | String          | True     | Unique log source identifier for QRadar.                                               |
