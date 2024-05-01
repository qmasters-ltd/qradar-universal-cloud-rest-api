# Cyberint-Argos API connector for QRadar

## How to Generate Cyberint API token

1. Log on to your Cyberint instance through: https://\<MyCompuny>/cyberint.io.

2. At the top right of the screen press the profile button and then enter the "USER SETTINGS".

3. In the user settings press at three dots in the top right.

4. Press the "Generate API Token" button.

5. Here you can see your API token.

## QRadar Log Source Configuration
A workflow XML document defines the behavior of the Universal Cloud REST API protocol. To ingest data from an endpoint through the Universal REST API protocol, you can create a log source on the QRadar® Console using the Log Source Management app. In the Workflow field of the log source, you can specify how the endpoint can communicate with QRadar using the Universal REST API protocol.

The parameters XML document specifies the user settings for this log source, including API authentication and relevant configurations.

1. Log in to QRadar and click the admin panel.

2. To create DSM, click the DSM editor app icon.

3. Then click Create New and insert the name (_Cybeirnt API_).

4. To create the log source, go to the admin panel and click the QRadar Log Source Management app icon.

5. Click New Log Source > Single Log Source.

6. On the Select a Log Source Type page, Select a Log Source Type Cyberint API.

7. On the Select Protocol Type page, select Universal Cloud REST API, and go to Step 3.

8. On the Configure the Log Source parameters page, configure the log source name and click Configure Protocol Parameters.

9. On the Configure the Protocol Parameters page, configure the protocol-specific parameters:
 - Insert a log source identifier - "Cyberint Domain Name";
 - Copy the Workflow XML you downloaded from GitHub and paste it into the Workflow field;
 - Copy the Workflow Params (make sure your domainName and api_key are populated) into the Workflow Parameters Values field;
 - **Make sure to turn off the Coalescing Events to avoid grouping of the events on the basis of Source and Destination IP.**

11. In the Test protocol parameters window, click Start Test.

12. To fix any errors, click Configure Protocol Parameters. Configure the parameters and click Test Protocol Parameters.

13. Click Finish

## CyberInt Parameters Configuration
Parameter                           | Name | Default Value | Type | Required (True/False) | Description
---                                 | --- | --- | --- |--- |---
domainName                            | Domain Name | https://\<MyCompuny>.cyberint.io | String | True | Domain of your Cyberint instance.
apiKey                             | API Key | False | Authentication | True | Cyberint API token for QRadar.
severity                            | Severity | "very_high" "high", "medium", "low" | Array of String | False | You can specify the alert severity to pull.
status                              | Status | "open", "acknowledged", "closed" | Array of String | False | You can specify the alert status to pull.
timeZone                            | Time Zone  | UTC      | String         | No             | Time zone selection.
