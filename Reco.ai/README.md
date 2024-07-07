Reco-AI Alerts Connector for QRadar
Getting the Reco-AI API Key
Step 1: Accessing the Reco-AI Cloud Console
	1. Navigate to Integration: In the Reco-AI cloud console, select the "Integrations" option under "Configurations".
	2. API Keys: Click on API Keys to proceed to the management area for API Keys.
	3. Add API Keys: On the API Keys Management page, choose Add to create a new client application.
	4. Name the Application: Provide a name for your client application and confirm by clicking Add.
	5. Save the generated API Key, and insert it in the "WorkflowParameter" XML.
	7. Completion: Click OK to complete the process.

Ensure you store the API Key securely as it provides authenticated access to the Reco-AI services. It's essential for integrating Reco-AI with QRadar or other security information and event management (SIEM) platforms.
For further details on managing client applications or using the API, refer to the Reco-AI Documentation.
Configuring the Reco-AI Connector in QRadar.
To configure the Reco-AI Alerts Connector in QRadar, follow these steps to fill in the necessary parameters in the workflow parameter file:
	1. identifier [REQUIRED]: The log source identifier to post the events to. This should be a unique identifier for the Reco-AI log source in QRadar.
	2. base_url [REQUIRED]: The base URL for the Reco-AI API endpoint. This is typically the main URL for the Reco-AI service. It should be entered without "https://".
	3. api_key [REQUIRED]: The API key obtained from the Reco-AI cloud console. This key is necessary for authenticated access to the Reco-AI services.
	4. time_zone [OPTIONAL] [DEFAULT=UTC]: The time zone to be used in the Reco-AI. The default is UTC, but you can set it to any valid time zone. For example, "GMT+3".
	5. initial_fetch_period [OPTIONAL] [DEFAULT=7]: The number of days in the past from which events will be initially retrieved. The default is 7 days.

After configuring the "WorkflowParameterValues" XML file with the appropriate values, create a new DSM for Reco-AI which will pull event using Universal Cloud API protocol. Upload the workflow and workflow parameter to QRadar and activate the Reco-AI Alerts Connector. This will enable QRadar to retrieve and process alert logs from Reco-AI, enhancing your security information and event management capabilities.

For further assistance or detailed configuration options, refer to the Reco-AI Documentation/Support.