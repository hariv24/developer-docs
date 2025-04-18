---
description: A plugin that lookups timesheet information based of a project.
fidelity: GUIDE
difficulty_level: BEGINNER
time_in_minutes: 15
name: 'Lookup Timesheet Information '
purple_chat_link: https://developer.moveworks.com/creator-studio/developer-tools/purple-chat?conversation=%7B%22startTimestamp%22%3A%2211%3A43+AM%22%2C%22messages%22%3A%5B%7B%22role%22%3A%22user%22%2C%22parts%22%3A%5B%7B%22richText%22%3A%22Can+you+pull+my+timesheet+data+for+project+Hydrogen%3F%22%7D%5D%7D%2C%7B%22role%22%3A%22assistant%22%2C%22parts%22%3A%5B%7B%22reasoningSteps%22%3A%5B%7B%22status%22%3A%22success%22%2C%22richText%22%3A%22%3Cp%3E%E2%9C%85+Working+on+%3Cb%3EPull+Timesheet+Data%3C%2Fb%3E%3Cbr%3E%E2%8F%B3+Calling+Plugin+%3Cb%3ELookup+Time+Sheet+Information%3C%2Fb%3E%3C%2Fp%3E%22%7D%5D%7D%2C%7B%22richText%22%3A%22You%27ve+spent+%3Cb%3E120+hours%3C%2Fb%3E+on+project+Hydrogen+this+month.+Do+you+need+detailed+timesheet+entries+or+any+other+project+data%3F%22%7D%5D%7D%5D%7D
solution_tags:
- HR
- HR - Time & Absence
systems:
- sap-success-factors

---


# **Introduction :**

The **SAP_Lookup_Timesheet_Information** plugin allows users to retrieve a list of timesheets information from SAP SuccessFactors directly through the Moveworks AI Assistant. With this plugin, users can quickly access timesheet information of user.

This guide will help you install and configure the plugin in Agent Studio within minutes. Let’s get started!

# Prerequisites :

- Access to Agent Studio
- [SAP Successfactors Connector](https://developer.moveworks.com/creator-studio/resources/connector/?id=sap-success-factors&commit_id=21f2fb0f5f2b0852c62a72235121cd8d78d6b46b;) built in Creator Studio (follow the SAP  Successfactors  Authentication guide to create your connector)

# What are we building?

## **Agent Design**

This [purple chat](https://developer.moveworks.com/creator-studio/developer-tools/purple-chat?conversation=%7B%22startTimestamp%22%3A%2211%3A43+AM%22%2C%22messages%22%3A%5B%7B%22role%22%3A%22user%22%2C%22parts%22%3A%5B%7B%22richText%22%3A%22Can+you+pull+my+timesheet+data+for+project+Hydrogen%3F%22%7D%5D%7D%2C%7B%22role%22%3A%22assistant%22%2C%22parts%22%3A%5B%7B%22reasoningSteps%22%3A%5B%7B%22status%22%3A%22success%22%2C%22richText%22%3A%22%3Cp%3E%E2%9C%85+Working+on+%3Cb%3EPull+Timesheet+Data%3C%2Fb%3E%3Cbr%3E%E2%8F%B3+Calling+Plugin+%3Cb%3ELookup+Time+Sheet+Information%3C%2Fb%3E%3C%2Fp%3E%22%7D%5D%7D%2C%7B%22richText%22%3A%22You%27ve+spent+%3Cb%3E120+hours%3C%2Fb%3E+on+project+Hydrogen+this+month.+Do+you+need+detailed+timesheet+entries+or+any+other+project+data%3F%22%7D%5D%7D%5D%7D) shows the experience we are going to build.

# **Installation Steps**

While you can create a connector during plugin installation, we recommend creating a connector in **Agent Studio** beforehand to streamline the process. Please follow our **SAP successfactors Connector Guide** to do so. Once completed, follow our plugin installation documentation to install the **SAP_Lookup_Timesheet_Information** plugin in minutes.

After configuring the connector, refer to our installation documentation for more details on completing the setup.

# **Appendix**

## API #1: **Fetch UserId using User Email**

The **SAP_Lookup_Timesheet_Information** API retrieves a userId using user email.

```bash
curl --request GET
--location 'https://<API_SERVER>/odata/v2/User?%24top=30&%24filter=email%20eq%20%27<email>%27%20&%24select=defaultFullName%2Cemail%2CempId%2CfirstName%2CuserId%2C%20username%2CassignmentUUID%2Cmanager' \
--header 'Authorization: Bearer <ACCESS_TOKEN>' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
```

**Path Parameters:**

- `<email>`  (string) – The email of the user whose timesheet information you want to retrieve. This would be provided user ID of the user.

**Query Parameters :**

- $filter (string) ****– Filter items by property values
- $select (array[string]) – Select properties to be returned
- `optional_fields`(string) – Specify additional fields to include in the response, such as $top,$skip

## API #2: **Fetch Timesheet Information using UserId**

```bash
curl --request GET
--location '<API_SERVER>/odata/v2/User('\''<userId>'\'')/userIdOfEmployeeTimeSheetNav?%24top=10&%24skip=5&%24expand=employeeTimeSheetEntry&%24select=approvalStatus%2Cperiod%20%2CrecordedHoursAndMinutes%2CplannedHoursAndMinutes%2CexternalCode&%24orderby=period%20desc' \
--header 'Authorization: Bearer <ACCESS_TOKEN>' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \

```

**Path Parameters:**

- `<userId>` (integer) – The userId of the user whose timesheet you want to retrieve. This would be provided list of timesheet information of the user.

**Query Parameters :**

- $expand (array[string]) ****– Expand related entities
- $select (array[string]) – Select properties to be returned,
- $orderby (array[string]) – Order items by property values
- `optional_fields`(string) – Specify additional fields to include in the response, such as $top,$skip