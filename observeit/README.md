# ObserveIT Parameters Configuration
| Parameter                        | Name                                         | Required (True/False) | Type            | Description                                                                                               | Default Value |
|----------------------------------|----------------------------------------------|-----------------------|-----------------|-----------------------------------------------------------------------------------------------------------|---------------|
| `identifier`                     | Log Source Identifier                        | True                  | String          | The log source identifier to post the events to.                                                          |               |
| `hostname`                       | Host Name                                    | True                  | String          | IP for the instance.                                                                                      | `https://myObserveIT.com` |
| `client_id`                      | Organization Key                             | True                  | Authentication  | Can be received through the Developer Portal by selecting Credentials and pressing the Create App button. |               |
| `client_secret`                  | API Secret                                   | True                  | Authentication  | Can be received through the Developer Portal by selecting Credentials and pressing the Create App button. |               |
| `time_zone`                      | Time Zone                                    | False                 | String          | The timezone used in ObserveIT.                                                                           | `UTC`         |
| `events_per_poll`                | Events Per Poll                              | False                 | Number          | Max number of records to return per poll. Note: a large fetch may cause timeout errors.                   | `100`         |
| `initial_event_fetch_period`     | Initial Event Fetch Period in Days           | False                 | Number          | Number of days in the past from which events will be initially retrieved.                                 | `7`           |
| `report_type`                    | Report Type                                  | True                  | String          | The report type to poll. One of:<br>`alert_v0`,<br>`audit_configuration_v0`,<br>`audit_logins_v0`,<br>`audit_saved_sessions_v0`,<br>`audit_session_playback_v0`,<br>`system_events_v0`,<br>`user_command_activity_with_output_v0`,<br>`user_command_output_stream_v0`,<br>`user_dba_activity_v0`,<br>`user_file_activity_v0`,<br>`user_interface_activity_v0`,<br>`user_messaging_actions_activity_v0`,<br>`user_session_v0`. |               |
| `piis_to_exclude`                | Personal Identifiable Information to Exclude | False                 | String          | Comma-separated list of Personal Identifiable Information (PII) to exclude.                               | `loginName`, `secondaryLoginName`, `endpointName`, `remoteHostName`, `windowTitle`, `accessedUrl`, `domainName`, `secondaryDomainName`, `remoteAddress`, `sqlUserName`, `sessionServerName`, `sessionLoginName`, `savedSessionName`, `operatorUsername`, `operatorDomainName`, `userName`, `machineName` |
| `sleep_time_in_seconds`          | Sleep Time in Seconds                        | False                 | Number          | The downtime for the connector after it is in sync with the server (Min: 0).                              | `20`          |
| `debug_mode`          | Debug Mode                        | False                 | String          | Set to `true` in case you want to get debug logs as event logs.                              | `false`          |

# How to Generate Client ID and Client Secret
1. Log on to your ObserveIT instance through: https://\<MyObserveIT>/ObserveIT.

2. At the top right of the screen press the "?" button and then enter the "Developer Portal".

3. In the Developer Portal enter "🔒 Credentials".

4. Press the "+ Create App" button.

5. Enter an "Application Name".

6. Press your application's name.

7. Here you can see your Client ID and Client Secret.


# QRadar Log Source Configuration
If you want to ingest data from an endpoint using Universal Rest API Protocol, configure a log source on the QRadar® Console using the Workflow field so that the defined endpoint can communicate with QRadar by using the Universal Rest API protocol.

1. Log in to QRadar.

2. Click the Admin tab.

3. To create DSM, click the DSM editor app icon.

4. Then click Create New and name it "ObserveIT API".

4. To create the log source, click the QRadar Log Source Management app icon.

5. Click New Log Source > Single Log Source.

6. On the Select a Log Source Type page, Select a Log Source Type ObserveIT API and click Select Protocol Type (Universal Rest API).

7. On the Select a Protocol Type page, select a protocol and click Configure Log Source Parameters.

8. On the Configure the Log Source parameters page, configure the log source parameters and click Configure Protocol Parameters.

9. On the Configure the Protocol Parameters page, configure the protocol-specific parameters (Workflow and Workflow Parameter Values).

10. In the Test protocol parameters window, click Start Test.

10. To fix any errors, click Configure Protocol Parameters. Configure the parameters and click Test Protocol Parameters.

11. Click Finish

- The log source identifier must be identical to the inserted `hostname`.
- Copy the Workflow XML into the Workflow field.
- Populate the Workflow Parameters according to the table above and copy it into the Workflow Parameters Values field.
- Make sure to turn off the Coalescing Events to avoid grouping of the events on the basis of Source and Destination IP.
- It is advised to open an individual log source for report types that fetch large amount of data.
