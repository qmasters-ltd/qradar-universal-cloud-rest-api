# Symantec-ICD Incidents Connector for QRadar

## Getting the Symantec Endpoint Security API Key

### Step 1: Accessing the Symantec ICDm Cloud Console

1. **Navigate to Integration**: In the Symantec ICDm cloud console, select the `Integration` option.

2. **Client Applications**: Click on `Client Applications` to proceed to the management area for client applications.

3. **Add Client Application**: On the Client Application Management page, choose `Add` to create a new client application.

4. **Name the Application**: Provide a name for your client application and confirm by clicking `Add`.

5. **Generate Client Secret**: Find the newly created Client Application, click the More menu (indicated by ellipses), and select `Client Secret`.

6. **Copy OAuth Credentials**: Next to the OAuth Credentials, use the Copy icon to copy the client secret to your clipboard.

7. **Completion**: Click `OK` to complete the process.

Ensure you store the Client Secret securely as it provides authenticated access to the Symantec Endpoint Security services. It's essential for integrating Symantec Endpoint Security with QRadar or other security information and event management (SIEM) platforms.

For further details on managing client applications or using the API, refer to the [Symantec Documentation](https://apidocs.securitycloud.symantec.com/#).


### QRadar Log Source Configuration for Symantec-ICD

To integrate Symantec-ICD with QRadar for data ingestion, follow these steps to configure the log source:

1. **Access QRadar**: Log into your QRadar system and navigate to the admin panel.

2. **DSM Creation**: Open the DSM editor app and select "Create New". Name it appropriately, for example, "Symantec-ICD".

3. **Log Source Setup**: Go to the QRadar Log Source Management app within the admin panel and initiate a new log source setup.

4. **Select Log Source Type**: Choose "Single Log Source" and for the log source type, select "Symantec-ICD".

5. **Protocol Selection**: When prompted for the protocol type, select "Universal Cloud REST API".

6. **Configure Log Source**: Enter a memorable name for the log source and proceed to configure protocol parameters.

7. **Protocol Parameters Configuration**:
   - Use the instance name and API key from your Symantec-ICD account to configure the connection.
   - Input the customized workflow XML tailored for Symantec-ICD integration, ensuring fields such as `api_key`, `time_zone`, and `events_per_fetch` are correctly populated.

8. **Testing**: Use the test functionality to verify the connection and data retrieval from Symantec-ICD.

9. **Finish Configuration**: Finalize the setup and start monitoring Symantec-ICD events within QRadar.

### Symantec-ICD Parameters Configuration

| Parameter              | Description                                       |
|------------------------|---------------------------------------------------|
| `identifier`           | The log source identifier for Symantec-ICD.       |
| `instance_name`        | The Symantec-ICD API instance name.                   |
| `api_key`              | The API key for authenticating with Symantec-ICD. |
| `time_zone`            | The time zone used for log timestamps.            |
| `events_per_fetch`     | Maximum number of records retrieved per fetch.    |
| `initial_fetch_period` | Lookback period for initial event retrieval.      |

This guide aims to streamline the integration process of Symantec-ICD with QRadar, ensuring a smooth data ingestion flow for better threat management and analysis.
