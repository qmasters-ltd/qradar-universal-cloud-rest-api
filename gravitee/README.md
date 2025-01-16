# Gravitee.io API Connector for QRadar

# How to Generate Gravitee.io API Token
1. Log in to your Gravitee.io API Management console.
2. Navigate to **Settings** > **API Tokens**.
3. Click **Create API Token**.
4. Enter a meaningful and concise label for your token and click **Generate**.
5. Copy the generated token and store it securely.

# QRadar Log Source Configuration
A workflow XML document defines the behavior of the Universal Cloud REST API protocol. To ingest data from an endpoint through the Universal REST API protocol, you can create a log source on the QRadar® Console using the Log Source Management app. In the Workflow field of the log source, you can specify how the endpoint can communicate with QRadar using the Universal REST API protocol.

The parameters XML document specifies the user settings for this log source, including API authentication and relevant configurations.

1. Log in to QRadar and go to the **Admin** panel.
2. To create DSM, click the **DSM Editor** app icon.
3. Click **Create New** and enter the name (_Gravitee API_).
4. To create the log source, navigate to the **Admin** panel and click the **QRadar Log Source Management** app icon.
5. Click **New Log Source** > **Single Log Source**.
6. On the **Select a Log Source Type** page, select **Gravitee API**.
7. On the **Select Protocol Type** page, select **Universal Cloud REST API**.
8. On the **Configure the Log Source Parameters** page, configure the log source name and click **Configure Protocol Parameters**.
9. On the **Configure the Protocol Parameters** page, configure the protocol-specific parameters:
   - Insert a log source identifier (_Gravitee API_);
   - Copy the **Workflow XML** downloaded from GitHub and paste it into the **Workflow** field;
   - Copy the **Workflow Parameters** (ensure `api_host`, `api_token`, and `identifier` are populated) into the **Workflow Parameters Values** field;
   - **Make sure to turn off the Coalescing Events to avoid grouping of the events based on Source and Destination IP.**
10. In the **Test Protocol Parameters** window, click **Start Test**.
11. If any errors occur, click **Configure Protocol Parameters**, modify the parameters, and click **Test Protocol Parameters**.
12. Click **Finish**.

# Gravitee.io Parameters Configuration

Parameter               | Name                           | Default Value                      | Type         | Required (True/False) | Descriptsion
------------------------|--------------------------------|------------------------------------|--------------|-----------------------|-------------------------------------------------------------
api_host               | Gravitee API Host              | N/A                                | String       | True                  | Gravitee API host URL.
api_token              | Gravitee API Token            | N/A                                | Authentication | True                  | API token for accessing Gravitee audit logs.
org_id                 | Organization ID               | DEFAULT                            | String       | False                 | Organization ID (default: DEFAULT).
env_id                 | Environment ID                | DEFAULT                            | String       | False                 | Environment ID (default: DEFAULT).
identifier             | Log Source Identifier         | Gravitee API                      | String       | True                  | The log source identifier for QRadar.
filter_environment     | Filter by Environment         | N/A                                | String       | False                 | Filter logs by environment.
filter_api             | Filter by API                 | N/A                                | String       | False                 | Filter logs by API.
filter_application     | Filter by Application         | N/A                                | String       | False                 | Filter logs by application.
filter_type           | Filter by Audit Type         | N/A                                | String       | False                 | Filter logs by audit type (e.g., ORGANIZATION, ENVIRONMENT, APPLICATION, API).
filter_event          | Filter by Event               | N/A                                | String       | False                 | Filter logs by event.
max_results           | Max Results                   | 100                                | Integer      | False                 | Maximum number of audit logs to retrieve per poll.
initial_event_fetch_period | Initial Event Fetch Period | 7                                  | Integer      | False                 | Start time for log retrieval in epoch time (default: past 7 days).