# QRadar Universal Cloud Rest API

<h1 align="center">
  <img width="auto" height="50px" src="https://awsmp-logos.s3.amazonaws.com/28ee383e-9c31-4664-a692-a00a472feb1c/08243c42094d411568f25ffd5ae3e1e9.png"/>
  <img width="auto" height="50px" src="https://assets.extrahop.com/images/logos/ibm-qradar.png"/>
</h1>


## IBM QRadar Universal Cloud Connector
The QRadar Universal Cloud REST API is a powerful feature that helps enhance visibility by easily gathering data from a wide range of REST API cloud-based applications and services. With the Universal Cloud REST API Protocol, users can create log sources for REST API compatible data sources that are not currently supported officially by IBM. This allows organizations to quickly and easily connect to cloud-based or on-premise endpoints that were previously inaccessible.

The Universal Cloud REST API Protocol includes pre-configured workflows for select data sources, which can significantly reduce the time required to create new log sources. Moreover, users can tailor the data to their specific use cases by defining normalized properties, classifying event data, and extracting custom event properties using the DSM Editor.
By connecting their data sources with the Universal Cloud REST API Protocol, organizations can enhance their threat detection capabilities, and analysts can easily access critical investigation information in their workspace using QRadar's Analyst Workflow. This minimizes the need to navigate elsewhere for additional context. In summary, the QRadar Universal Cloud REST API is a powerful tool that helps organizations adapt to the ever-changing digital landscape and improve their security posture.


## Supported version
Universal Cloud REST API protocol is supported on QRadar 7.3.2 or later, and the QRadar Log Source Management app must be installed.
- See: [Universal Cloud REST API protocol - IBM Documentation](https://www.ibm.com/docs/en/qsip/7.4?topic=configuration-universal-cloud-rest-api-protocol)


## Terminology
#### Universal Cloud Rest Api terms:

Workflow: An XML document that outlines the event retrieval process. It defines one or more parameters, which can have assigned values within the XML or derive values from the Workflow Parameter Values XML document. The Workflow consists of several actions that run sequentially. When the Workflow is initiated, the parameter values are included in the State. As the Workflow progresses, actions can access and modify the State.

Workflow Parameter Values: The input parameters for a Workflow instance, stored in an XML file. These values consist of key/value pairs, and each key must match a parameter defined in the corresponding Workflow.


## Authors
At QMasters, we believe in giving back to the community and our customers. As a team that has worked extensively with SIEMs since the beginning of our journey, we understand the importance of data for effective threat detection and response. We collaborate closely with our customers and vendors to provide them with the tools they need to maximize their security data. By developing and sharing tools like the QRadar Universal Cloud REST API, we aim to contribute to the broader security community and help organizations enhance their security posture. Visit us at: www.qmasters.co 


## Contributing
We welcome contributions from the community to improve QRadar Universal Cloud REST API. 
If you have ideas for new features, enhancements to existing features, or bug fixes, please feel free to submit a pull request.

Before submitting a pull request, make sure to review our contributing guidelines, which outline the process for submitting contributions and offer helpful tips on how to get started.

Thank you for helping improve the QRadar Universal Cloud REST API and contributing to the security community!


## Useful Links

 - [IBM GitHub](https://github.com/IBM/IBM-QRadar-Universal-Cloud-REST-API)
 - [Universal Cloud REST API protocol](https://www.ibm.com/docs/en/qsip/7.4?topic=configuration-universal-cloud-rest-api-protocol)


## Support
To request support or suggest the development of new features for the QRadar Universal Cloud Rest API, please contact our support team at support@qmasters.co.