# GitHub API connector for QRadar

# How to Generate GitHub API Token
1. **Log in**: Visit [GitHub](https://github.com/) and log in to your account as an organization owner.

2. **Access Settings**: Click on your profile picture > "Settings".

3. **Developer Settings**: Click "Developer settings" in the left sidebar.

4. **Generate Token**: Under "Personal access tokens," click "Generate token."

5. **Configure Token**:
   - Enter a name for your token in the "Note" field.
   - Scroll down and find "read:audit_log" in the scopes list, then check the checkbox.

6. **Generate**: Click "Generate token" at the bottom of the page.

7. **Copy Token**:
   - Copy the generated token (only shown once).
   - Click "Copy" to copy the token to your clipboard.

# QRadar Log Source Configuration
A workflow XML document defines the behavior of the Universal Cloud REST API protocol. To ingest data from an endpoint through the Universal REST API protocol, you can create a log source on the QRadar® Console using the Log Source Management app. In the Workflow field of the log source, you can specify how the endpoint can communicate with QRadar using the Universal REST API protocol.

The parameters XML document specifies the user settings for this log source, including API authentication and relevant configurations.

1. Log in to QRadar and click the admin panel.

2. To create DSM, click the DSM editor app icon.

3. Then click Create New and insert the name (GitHub API).

4. To create the log source, go to admin panel and click the QRadar Log Source Management app icon.

5. Click New Log Source > Single Log Source.

6. On the Select a Log Source Type page, Select a Log Source Type GitHub API.

7. On the Select Protocol Type page, select Universal Cloud REST API.

8. On the Configure the Log Source parameters page, configure the log source name and click Configure Protocol Parameters.

9. On the Configure the Protocol Parameters page, configure the protocol-specific parameters:
 - Insert a log source identifier ,your GitHub "*orgName*" or your GitHub "*enerpriseName*";
 - Copy the Workflow XML you downloaded from GitHub and paste it into the Workflow field;
 - Copy the Workflow Params (make sure your OrgName, and apiToken are populated) into the Workflow Parameters Values field;
 - **Make sure to turn off the Coalescing Events to avoid grouping of the events on the basis of Source and Destination IP.**

10. In the Test protocol parameters window, click Start Test.

11. To fix any errors, click Configure Protocol Parameters. Configure the parameters and click Test Protocol Parameters.

12. Click Finish

# GitHub Parameters Configuration
| Parameter   | Name                  | Default Value          | Type           | Required | Description                                       |
| ----------- | --------------------- | ---------------------- | -------------- | -------- | ------------------------------------------------- |
| orgName     | GitHub Organization Name  |      | String         | Yes            | GitHub Organization Name.                        |
| enterpriseName     | GitHub Enterprise Name  |      | String         | Yes            | GitHub Enterprise Name.                        |
| apiToken    | GitHub API Token      |          | Authentication | Yes            | GitHub API token for QRadar.                     |
| phrase      | Search Phrase         |          | String         | No             | A search phrase.                                 |
| include     | Event Types to Include| all      | String         | No             | The event types to include: web, git, all.       |
| perPage     | Results Per Page      | 30       | Integer        | No             | Number of results per page (max 100).           |
| timeZone    | Time Zone             | UTC      | String         | No             | Time zone selection.                             |
| startTime   | Start Time            |          | Integer        | No             | Specify the start time to retrieve logs from. Provide the time in epoch time with milliseconds (e.g., 1693309396000). The default is logs from the past 1 hour.                             |
