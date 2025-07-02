# Gravitee.io API Connector for QRadar

Integrate **Gravitee.io API Management** API logs directly into **IBM QRadar** using the Universal Cloud REST API protocol. This guide explains how to generate your API token, configure QRadar, map required parameters, and understand the connector’s data collection workflow.

---

## 1. How to Generate a Gravitee.io API Token

1. Log in to your Gravitee.io API Management console.
2. Go to **Settings** → **API Tokens**.
3. Click **Create API Token**.
4. Enter a clear label and click **Generate**.
5. Copy and securely store your token (it won’t be shown again).

---

## 2. QRadar Log Source Configuration

You will use a **Workflow XML** to configure the Universal Cloud REST API protocol in QRadar for collecting Gravitee API logs.

### Steps

1. **Log in** to QRadar and go to the **Admin** panel.
2. Open the **DSM Editor** app and click **Create New**.  
   - Name: `Gravitee API Logs`
3. In the **Admin** panel, open the **QRadar Log Source Management** app.
4. Click **New Log Source** → **Single Log Source**.
5. On the **Select a Log Source Type** page, choose **Gravitee API**.
6. On the **Select Protocol Type** page, select **Universal Cloud REST API**.
7. On the **Configure the Log Source Parameters** page:
    - Enter a **log source name** (e.g., `Gravitee API Logs`).
    - Click **Configure Protocol Parameters**.
8. On the **Configure the Protocol Parameters** page:
    - Enter a log source identifier (e.g., `Gravitee-API-Logs`).
    - **Paste the Workflow XML** into the **Workflow** field.
    - **Paste the Workflow Parameters XML** (see below) into the **Workflow Parameters Values** field.
    - **Important:** *Turn off* "Coalescing Events" to avoid grouping events by Source and Destination IP.
9. Click **Test Protocol Parameters** and then **Start Test**.
10. If any errors occur, adjust the parameters and retest.
11. Click **Finish** when successful.

---

## 3. Gravitee.io Workflow Parameters Mapping

> **Note:**  
> The connector fetches all APIs from your Gravitee environment, then collects API logs for each API from the configured start time up to the present, paging results as defined by `max_results`.


Below are the supported parameters.  
**Bold fields are required.**

| Parameter                   | Name                    | Default Value | Type            | Required | Description                                                                                      |
|-----------------------------|-------------------------|---------------|-----------------|----------|--------------------------------------------------------------------------------------------------|
| **api_host**                | Host Name               | N/A           | String          | True     | Gravitee API Management host URL (e.g., `https://apim.company.com/management`)|
| **api_token**               | API Token               | N/A           | Authentication  | True     | API token for accessing Gravitee API logs.                                                       |
| org_id                      | Organization ID         | DEFAULT       | String          | False    | Organization ID (`DEFAULT` by default).                                                          |
| env_id                      | Environment ID          | DEFAULT       | String          | False    | Environment ID (`DEFAULT` by default).                                                           |
| identifier                  | Identifier              | Gravitee-API-Logs | String      | False    | Unique log source identifier for QRadar.                                                         |
| max_results                 | Page Size               | 100           | Integer         | False    | Maximum number of API logs to retrieve per poll.                                                 |
| initial_event_fetch_period  | Initial Event Fetch Period in Days | 7 | Integer (days)  | False    | How many days back to fetch API logs on first collection (default: 7 days).                      |

