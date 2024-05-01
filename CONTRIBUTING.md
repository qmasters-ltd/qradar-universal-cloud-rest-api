# Contributing
At QMasters, we believe in the power of community-driven innovation. As such, we welcome and encourage contributions from the community to help improve the IBM Qradar Eco system our thread for Universal Cloud REST API.

We have created a selection of workflows and are sharing them with the community, we understand that there might be specific use cases that we have not addressed. 
We welcome sharing, please use our platform and reach to share additional capabilities and workflows which will benefit others, we love feedback and  would love to hear from you!

## Code of Conduct
We expect all contributors to adhere to our code of conduct. This includes being respectful of others and their opinions, refraining from discriminatory or abusive language, and working collaboratively to achieve common goals.

## What to include:
Reference: IBM's Contribution Process

In order to to share a workflow and share via the master branch branch successfully, please ensure the following criteria is met before submitting:

**Ensure your README file fits the following template:**
- **Author Name:**
- **Maintainer Name:** (Github Alias of who any issues should be logged against for consideration)
- **Endpoint Documentation:**
    - Please provide a link to vendor documentation if available on the internet. if this is behind a portal, please provide at minimum a link to the portal it is behind.
- **Any other information pertaining to the workflow that the Author feels is important to convey**

**Ensure your code follows these guidelines:**
- **Ensure that Logging and Debugging messages are present in your code** - These messages are what allow users to verify what may be wrong with their code. As a general outline, we should be logging messages in the workflow at these points (but not limited to, based on the context of your workflow):
    - We combine fields, or translate them (such as taking a timestamp and formatting it)
    - We begin a query
    - We end a query - and how many events were returned
    - Any time we receive messages back from the endpoint we should try and capture non - authentication information into a comment
- Ensure that any complex processing is adequately commented for future maintainers / forkers to follow.
- Please Use camel casing for variable names (IE: newVariable)
- Please use indentation on opening and closing of XML tags to assist in readability, and use tab as the indentation character.
- Please try to name variables such that the names provide information about their usage - IE: "startTime" to identify the variable holding the timestamp the next query should begin at. 
- Ensure that any potentially sensitive user - provided parameters are set to secret.
- Please provide in your submission some obfuscated sample output of your workflow operating. This can be done by utilizing the workflow validation tool (https://www.ibm.com/docs/en/dsm?topic=protocol-command-line-testing-tool - with verbose output turned on).
    - **This information should be obfuscated before upload and have no PII / SPII within it**. We strictly want to see the proper operation of the workflow in the document. 

## To submit a workflow, please follow these steps:
- Fork the [qradar-universal-cloud-rest-api](https://github.com/qmasters-ltd/qradar-universal-cloud-rest-api)
- Create a new branch for your changes
- Add your workflow file(s) to the appropriate folder(s)
- Commit your changes and create a pull request

Once your pull request is reviewed and approved, we will post your workflow(s) here for others to use. We may also feature particularly innovative or useful workflows on our website or in our marketing materials.
