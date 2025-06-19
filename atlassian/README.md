# Atlassian API connector for QRadar

## How to Generate Atlassian API Key

### Prerequisites

Before you begin, make sure you have:

- An Atlassian account with organization owner privileges.


### Follow these steps to create an API key:

1. **Log in**: Visit [Atlassian](https://admin.atlassian.com/) and log in to your Atlassian account as an organization owner.

2. **Access Settings**: Once logged in, select your organization if you have more than one.

3. **API Keys**: Click on "Settings" in the top navigation menu.

4. **Create API Key**: Under "API keys," select "Create API key" in the top right corner.

5. **Name Your Key**:
   - Enter a name for your API key that you'll remember to identify it.

6. **Set Expiration Date (Optional)**:
   - By default, the key expires one week from today. If you'd like to change the expiration date, pick a new date under "Expires on." Note that you cannot select a date longer than a year from the date of creation.

7. **Create**: Click the "Create" button to save the API key.

8. **Copy Values**:
   - After creating the API key, you'll see the values for your Organization ID and API key displayed on the screen.
   - Copy both the Organization ID and API key. You'll need these values to use the API key.

**Note**: It's crucial to store these values in a safe place as they won't be displayed to you again.

**Important**: Keep your API key and Organization ID secure, as they provide access to your Atlassian resources and should not be shared or exposed in public repositories.

For more detailed information on tracking organization activities from the audit log using your Atlassian API key, please refer to the official [Atlassian Documentation](https://support.atlassian.com/security-and-access-policies/docs/track-organization-activities-from-the-audit-log/#Auditlogging-export).
.

## QRadar Log Source Configuration
A workflow XML document defines the behavior of the Universal Cloud REST API protocol. To ingest data from an endpoint through the Universal REST API protocol, you can create a log source on the QRadar® Console using the Log Source Management app. In the Workflow field of the log source, you can specify how the endpoint can communicate with QRadar using the Universal REST API protocol.

The parameters XML document specifies the user settings for this log source, including API authentication and relevant configurations.

1. Log in to QRadar and click the admin panel.

2. To create DSM, click the DSM editor app icon.

3. Then click Create New and insert the name (Atlassian API).

4. To create the log source, go to admin panel and click the QRadar Log Source Management app icon.

5. Click New Log Source > Single Log Source.

6. On the Select a Log Source Type page, Select a Log Source Type Atlassian API.

7. On the Select Protocol Type page, select Universal Cloud REST API.

8. On the Configure the Log Source parameters page, configure the log source name and click Configure Protocol Parameters.

9. On the Configure the Protocol Parameters page, configure the protocol-specific parameters:
 - Insert **your Atlassian org ID** as log source identifier;
 - Copy the Workflow XML you downloaded from Qmasters GitHub and paste it into the Workflow field;
 - Copy the Workflow Params (make sure your OrgID, and apiToken are populated) into the Workflow Parameters Values field;
 - **Make sure to turn off the Coalescing Events to avoid grouping of the events on the basis of Source and Destination IP.**

10. In the Test protocol parameters window, click Start Test.

11. To fix any errors, click Configure Protocol Parameters. Configure the parameters and click Test Protocol Parameters.

12. Click Finish

## Atlassian Parameters Configuration
| Parameter   | Name                  | Default Value          | Type           | Required | Description                                       |
| ----------- | --------------------- | ---------------------- | -------------- | -------- | ------------------------------------------------- |
| identifier             | Log Source Identifier         | Atlassian-AuditLogs                      | String       | True                  | The log source identifier for QRadar.
| orgID       | Atlassian Organization ID  |      | String         | Yes            | Atlassian Organization ID.                        |
| apiToken    | Atlassian API Token      |          | Authentication | Yes            | Atlassian API token for QRadar.                     |
| query      | Query         |          | String         | No             | Single query term for searching events.                                 |
| timeZone    | Time Zone             | UTC      | String         | No             | Time zone selection.                             |
| startTime   | Start Time            |          | Integer        | No             | Specify the start time to retrieve logs from. Provide the time in epoch time with milliseconds (e.g., 1693309396000). The default is logs from the past 1 hour.                             |
