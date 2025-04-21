# Dynamics 365 CRM Qradar Connector

## Dynamics 365 CRM Parameters Configuration

| Parameter              | Name                         | Required (True/False) | Type            | Description                                                                                          | Default Value     |
|------------------------|------------------------------|------------------------|------------------|------------------------------------------------------------------------------------------------------|-------------------|
| `identifier`           | Log Source Identifier        | True                   | String           | The log source identifier to post the events to in QRadar.                                           | `dynamics_365`    |
| `base_url`             | Base URL                     | True                   | String           | Base URL of the Dynamics 365 CRM instance. Example: `your-instance.crm.dynamics.com`                |                   |
| `client_id`            | Client ID                    | True                   | Authentication   | OAuth2 Client ID registered in Azure AD.                                                             |                   |
| `client_secret`        | Client Secret                | True                   | Authentication   | OAuth2 Client Secret associated with the above client ID.                                            |                   |
| `tenant_id`            | Tenant ID                    | True                   | Authentication   | Azure Active Directory (AD) Tenant ID under which the Dynamics 365 application is registered.       |                   |
| `crm_version`          | CRM Version                  | True                   | String           | Dynamics 365 CRM version (e.g., `9.1`, `9.2`). Used to determine feature and endpoint compatibility. |                   |
| `events_per_fetch`     | Events Per Fetch             | False                  | Number           | Maximum number of records to fetch in each API call. Large values may cause timeout errors.         | `1000`            |
| `initial_fetch_period` | Initial Fetch Period (Days)  | False                  | Number           | Number of days to look back when retrieving events initially.                                        | `7`               |

---

## QRadar Log Source Configuration for Dynamics 365 CRM

To ingest data using the Universal REST API Protocol, configure a log source on the QRadar Console with the appropriate workflow and parameter values.

### Steps:

1. Log in to QRadar.
2. Click the **Admin** tab.
3. Click the **DSM Editor** app icon to create a new DSM.
   - Click **Create New**, name it `Dynamics365CRM`.
4. Click the **Log Source Management** app icon.
5. Click **New Log Source > Single Log Source**.
6. On the **Select a Log Source Type** page:
   - Choose `Dynamics365CRM` as the Log Source Type.
   - Choose `Universal REST API` as the Protocol Type.
7. On the **Protocol Configuration** page:
   - Paste your Workflow XML into the **Workflow** field.
   - Paste the parameter configuration (see above) into the **Workflow Parameter Values** field.
   - Ensure **Coalescing Events** is turned **off**.
8. Click **Start Test** to verify.
9. If issues occur, click **Configure Protocol Parameters**, adjust, and **retest**.
10. Click **Finish** to save the log source.

---

## Notes

- The `identifier` in your Workflow Parameters must match the QRadar log source identifier.
- Ensure the Azure AD app has API permissions to access Dynamics 365 audit data.
- Open separate log sources for high-volume data types to improve performance.

---

## How to Register and Retrieve OAuth Token (Azure App)

1. Log into [Azure Portal](https://portal.azure.com).
2. Navigate to **Azure Active Directory** > **App Registrations**.
3. Click **New registration**, and complete app setup.
4. After creation, copy the **Client ID** and **Directory (Tenant) ID**.
5. Go to **Certificates & secrets** > click **New client secret**. Copy the secret value (it won't be shown again).
6. Assign the app appropriate API permissions to Dynamics 365.
7. Use these credentials in the `client_id`, `client_secret`, and `tenant_id` parameters.
