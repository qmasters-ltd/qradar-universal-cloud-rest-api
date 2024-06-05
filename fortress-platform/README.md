# Fortress API connector for QRadar

# How to Generate Fortress API token
1. Log on to your Fortress instanc.

2. At the left side of the screen press the settings button and then enter the "Admin Configuration".

3. In the Admin Configuration press at API Management.

4. Press the "+Add API key" button.

5. Insert the API name and choose the "View Alerts" permission, and press "Add".

6. Here you can see your api token.

# QRadar Log Source Configuration
A workflow XML document defines the behavior of the Universal Cloud REST API protocol. To ingest data from an endpoint through the Universal REST API protocol, you can create a log source on the QRadar® Console using the Log Source Management app. In the Workflow field of the log source, you can specify how the endpoint can communicate with QRadar using the Universal REST API protocol.

The parameters XML document specifies the user settings for this log source, including API authentication and relevant configurations.

1. Log in to QRadar and click the admin panel.

2. To create DSM, click the DSM editor app icon.

3. Then click Create New and insert the name (_Fortress API_).

4. To create the log source, go to admin panel and click the QRadar Log Source Management app icon.

5. Click New Log Source > Single Log Source.

6. On the Select a Log Source Type page, Select a Log Source Type Fortress API.

7. On the Select Protocol Type page, select Universal Cloud REST API, and go to Step 3.

8. On the Configure the Log Source parameters page, configure the log source name and click Configure Protocol Parameters. 

9. On the Configure the Protocol Parameters page, configure the protocol-specific parameters:
 - Insert a log source identifier (Fortress_API);
 - Copy the Workflow XML you downloaded from GitHub and paste it into the Workflow field;
 - Copy the Workflow Params (make sure your api_host, api_key and api_secret are populated) into the Workflow Parameters Values field;
 - **Make sure to turn off the Coalescing Events to avoid grouping of the events on the basis of Source and Destination IP.**

10. In the Test protocol parameters window, click Start Test.

11. To fix any errors, click Configure Protocol Parameters. Configure the parameters and click Test Protocol Parameters.

12. Click Finish

# Fortress Parameters Configuration
Parameter                           | Name | Default Value | Type | Required (True/False) | Description
---                                 | --- | --- | --- |--- |---
api_host                            | API Host | https://\<your instance> | String | True | URL for the instance.
api_id                              | API ID | False | Authentication | True | Fortress API id for QRadar
api_key                             | API Key | False | Authentication | True | Fortress API key for QRadar
severity                            | Severity | "CRITICAL", "HIGH", "MEDIUM", "LOW", "NONE" | array of strings | False | this parameter is an array of strings used to filter alerts by severity.
status                              | Status | "OPEN", "CLOSED", "DISMISSED", "QUARANTINED" | array of strings | False | this parameter is an array of strings used to filter alerts by status.
service_type                        | Service Type | "EDP", "MAIL", "CLOUD_STORAGE", "VMDR" | array of strings | False | this parameter is an array of strings used to filter alerts by service type.
page_size                           | page Size | 100 | integer | false | Max number of alerts to return per poll
time_zone                           | Time Zone | UTC | string | false | Select your time zone


# Fortress API Documentation
https://api-external.fortresscyber.io/
