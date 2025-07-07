# Tactical RMM Audit Logs Connector for QRadar

Integrate **Tactical RMM Audit Logs** into **IBM QRadar** using the Universal Cloud REST API protocol. This guide covers generating your API key, configuring QRadar, mapping workflow parameters, and understanding the connector’s data collection workflow.

---

## 1. How to Generate a Tactical RMM API Key

1. Log in to your **Tactical RMM** admin portal.
2. Navigate to **Settings** → **API Keys** or **Account Security**.
3. Click **Create API Key** (or equivalent).
4. Enter a descriptive name for the key and confirm permissions (read access to audit logs required).
5. Generate and **copy your API key**. Store it securely; it will not be shown again.

---

## 2. QRadar Log Source Configuration

You will use a **Workflow XML** to configure the Universal Cloud REST API protocol in QRadar for collecting Tactical RMM audit logs.

### Steps

1. **Log in** to QRadar and open the **Admin** panel.
2. Go to the **DSM Editor** and create a new DSM if required.
   - Name: `Tactical RMM Audit Logs`
3. In the **Admin** panel, open **QRadar Log Source Management**.
4. Click **New Log Source** → **Single Log Source**.
5. For **Log Source Type**, choose **Tactical RMM Audit** (or set a custom name).
6. For **Protocol Type**, select **Universal Cloud REST API**.
7. On the **Configure the Log Source Parameters** page:
    - Enter a **log source name** (e.g., `Tactical RMM Audit Logs`).
    - Click **Configure Protocol Parameters**.
8. On the **Configure the Protocol Parameters** page:
    - Enter a log source identifier (e.g., `Tactical-RMM-Audit`).
    - **Paste the Workflow XML** into the **Workflow** field.
    - **Paste the Workflow Parameters XML** (see below) into the **Workflow Parameters Values** field.
    - **Important:** *Turn off* "Coalescing Events" to avoid grouping events by Source and Destination IP.
9. Click **Test Protocol Parameters** and then **Start Test**.
10. Adjust parameters and retest if any errors are reported.
11. Click **Finish** once the configuration is successful.

---

## 3. Tactical RMM Audit Logs Workflow Parameters

> **Note:**  
> The connector fetches audit logs from the Tactical RMM system using the API. It supports time window selection and pagination to ensure all recent audit events are ingested into QRadar.

Below are the supported parameters.  
**Bold fields are required.**

| Parameter                   | Name                        | Default Value           | Type        | Required | Description                                                                                   |
|-----------------------------|-----------------------------|-------------------------|-------------|----------|-----------------------------------------------------------------------------------------------|
| **api_host**                | Host Name                   | https://api.yourunnstance.com | String   | True     | Tactical RMM API host for audit logs.                                                         |
| **api_key**                 | API Key                     | N/A                     | String      | True     | API Key for accessing Tactical RMM APIs (keep secure!).                                       |
| identifier                  | Identifier                  | Tactical-RMM-Audit      | String      | False    | Log source identifier for QRadar.                                                             |
| max_results                 | Page Size                   | 50                      | Integer     | False    | Number of audit events per API poll (can increase for higher throughput).                     |
| initial_event_fetch_period  | Initial Event Fetch Period in Days | 1                 | Integer     | False    | Number of days back to fetch audit logs on first collection (default: 1 day = last 24h).      |

