# Introduction

CICS Interdependency Analyzer Extension for Zowe Explorer adds additional functionality to the popular VS Code extension, [Zowe Explorer](https://github.com/zowe/vscode-extension-for-zowe "https://github.com/zowe/vscode-extension-for-zowe"). This extension allows users to interact and visualize CICS resources like Regions, Programs, Transactions and Webservices. 

CICS IA tool helps with runtime data collection for CICS Application. The CICS IA VS Code extension visualizes the collected data in the form meaningful to the user. 
# Contents
- [Privacy Notice for feedback](#privacy-notice-for-feedback)
- [Software Requirements](#software-requirements)
- [CICS IA Features](#cics-ia-features)
- [Installation](#installation)
- [Getting Started](#getting-started)
   - [Connecting using a CICS IA profile](#connecting-using-a-cics-ia-profile) 
   - [Loading CICS IA profiles from CICS profiles](#loading-cics-ia-profiles-from-cics-profiles)
   - [Create or Update CICS IA Profile](#create-or-update-cics-ia-profile)
   - [Delete CICS IA Profile](#delete-cics-ia-profile)
- [CICS IA Collector View](#cics-ia-collector-view)
- [CICS IA Profile](#cics-ia-profile)
- [Collection IDs](#collection-ids)
- [Regions](#regions)
    - [Regions Menu](#regions-menu)
- [Webservices](#webservices)
    - [Webservices Menu](#webservices-menu)
- [Transactions](#transactions)
    - [Transactions Menu](#transactions-menu)
- [Programs](#programs)
    - [Programs Menu](#programs-menu)
- [User Command Flow](#user-command-flow)
    - [User Command Flow Menu](#user-command-flow-menu)
- [Reports](#reports)
    - [Reports Menu](#reports-menu)
- [Program details view](#program-details-view)
- [Show Resources view](#show-resources-view)
- [Resource Usage Visualization view](#resource-usage-visualization-view)
- [Comparision of Resources](#comparision-of-resources)
- [Program Flow Editor](#program-flow-editor)
- [Used By view](#used-by-view)
- [Uses view](#uses-view)
- [Affinities view](#affinities-view)
- [Affinities Report view](#affinities-report-view)
- [Threadsafe Report view](#threadsafe-reports-view)
   - [Program Summary](#program-summary)
   - [Program Details](#program-details)
- [Command Flow view](#command-flow-view)
   - [TCB Modes Used](#tcb-modes-used)
   - [TCB Mode Switches](#tcb-mode-switches)
   - [Command flow table](#command-flow-table)
- [Command Flow Diagram view](#command-flow-diagram-view)
- [Report Browser view](#report-browser-view)
- [Creating a report of threadsafe issues](#creating-a-report-of-threadsafe-issues)
   - [ThreadSafe Report Procedure](#threadsafe-report-procedure)
- [Creating an affinity report](#creating-an-affinity-report)
   - [Affinity Report Procedure](#affinity-report-procedure)

## Privacy Notice for feedback
CICS Interdependency Analyzer Extension is provided free of charge, but we ask you to provide us feedback via the various means available, such as submitting an [issue in our GitHub repository](https://github.com/IBM/cics-ia-vs-code-extension/issues), submitting review comments in the [VS Code Marketplace](https://marketplace.visualstudio.com/items?itemName=ibm.cics-ia-extension-for-zowe#review-details).

You can also read [IBM's General Privacy Statement](https://www.ibm.com/privacy/us/en/) to learn more about our policies.

## Software Requirements
Ensure that you meet the following prerequisites before you use the extension:

- Install VSCode 1.93.0 or earlier versions
- Install Zowe Explorer v3
- Install Zowe CICS Explorer v3
- REST API preconfigured and running in the mainframe machine. Refer <https://www.ibm.com/support/pages/node/6378374> for REST API configuration for CICS IA.

## CICS IA Features
- Load profiles directly from ZOWE CICS VS code extension.
- Create new or Update existing Zowe CICS IA profiles and connect to them.
- Identify Collection IDs for which dependency or affinity data has been collected under a CICS IA profile.
- For every Collection ID, displays tree hierarchy of CICS resources like Regions, Programs, Transactions and Webservices.
- Filter and display the Programs, Transactions or web services used in a selected region.
- For every Transaction, Program or web service, you can view where it is used, regions associated with it and what resources it uses.
- View the tasks in a transaction.
- View the properties of a Program.
- Analyse the interdependencies between CICS Resources.
- Create and view summary or detail report of Threadsafe issues for a specific Program or Transaction or Region.
- Analyse the Transaction and system Affinities from a Transaction or Programs and also lists the details about Program, transaction and Command causing the affinities.
- View the execution details and timeline of Commands Collected by Command flow collector for a selected task.

To Install CICS Extension for Zowe Explorer see [Installation](#installation "https://github.com/zowe/cics-for-zowe-client/blob/HEAD/docs/installation-guide.md")

## Installation
Users can install Zowe Explorer CICS IA Extension from a VSIX file.
Execute the following steps to install the extension:
- Download cics-ia-extension-for-zowe.vsix file to your PC.
- Open VS Code and Click on the **Extensions** icon in the side bar.

    ![](https://github.com/IBM/cics-ia-vs-code-extension/raw/HEAD/docs/images/CICSIA.Words.2521e191-aa0c-43da-8799-3d24aab9b5d3.001.png)

- Click on the icon   and select the Install from VSIX… option..

    ![](https://github.com/IBM/cics-ia-vs-code-extension/raw/HEAD/docs/images/CICSIA.Words.2521e191-aa0c-43da-8799-3d24aab9b5d3.002.png)

- Browse the VSIX file location.
- Select the vsix file and click the Install button

    ![](https://github.com/IBM/cics-ia-vs-code-extension/raw/HEAD/docs/images/CICSIA.Words.2521e191-aa0c-43da-8799-3d24aab9b5d3.003.png)

   NOTE: The installation process will take a few seconds to complete.
- The "Completed installing Zowe Explorer for IBM CICS Interdependency Analyzer" message appears at the bottom right after successful installation.

    ![](https://github.com/IBM/cics-ia-vs-code-extension/raw/HEAD/docs/images/CICSIA.Words.2521e191-aa0c-43da-8799-3d24aab9b5d3.004.png)

- The CICS IA node appears in the primary sidebar of the Zowe extension activity bar in VS Code

    ![](https://github.com/IBM/cics-ia-vs-code-extension/raw/HEAD/docs/images/CICSIA.Words.2521e191-aa0c-43da-8799-3d24aab9b5d3.005.png)

## Getting Started
Follow the steps below to configure Zowe CICS IA Explorer.

## Connecting using a CICS IA profile

CICS IA (CICS Interdependency Analyzer) profiles are specialized Zowe profiles. They manage connections to a CICS IA DB2 server and a CICS IA REST API server. 

This allows users to access and interact with CICS IA data. CICS IA profiles are stored with other Zowe profiles in team configuration JSON files, making them easily shareable and manageable within development teams.
A CICS IA profile is a JSON object with specific properties that define the connection to the CICS IA DB2 database and the REST API. Key properties include:

The cicsia profile defines a connection with specific properties:
    
**Type**: Must be `"cicsia"`.

## Properties
The configuration is defined by an object with the following properties:

| Property                | Description                                                                 |
|-------------------------|-----------------------------------------------------------------------------|
| `db2HostName`          | The hostname for the DB2 server.                                            |
| `db2PortNumber`        | The port number for the DB2 server.                                         |
| `db2Location`          | The DB2 location name.                                                      |
| `iaApiHostName`        | The hostname for the CICS IA REST API.                                      |
| `iaApiPortNumber`      | The port for the CICS IA REST API.                                          |
| `schema`               | The name of the DB2 schema containing CICS IA data.                         |
| `name`                 | A name for the existing CICS profile you're connecting to.                  |
| `user`                 | The username for authenticating to the DB2 server.                          |
| `password`             | The password for the DB2 user.                                              |
| `rejectUnauthorized`   | A boolean (`true` or `false`) to control whether self-signed certificates are rejected. |


Similar to other Zowe profiles, CICS IA profiles support inheritance. This means they can inherit common properties from a base profile, which reduces redundancy and ensures consistency across multiple configurations.

## Loading CICS IA profiles from CICS profiles
- By Default, CICS profiles from CICS VS Code extension is loaded into CICS IA View.
- Find link for creating a new CICS profile Create CICS Profile
    https://marketplace.visualstudio.com/items?itemName=Zowe.cics-extension-for-zowe#connecting-using-a-cics-profile

- After Creating a new CICS Profile refresh CICS IA view, we should be able to see the newly created CICS profile getting loaded automatically under CICS IA view as well.

    ![](https://github.com/IBM/cics-ia-vs-code-extension/raw/HEAD/docs/images/CICSIA.Words.2521e191-aa0c-43da-8799-3d24aab9b5d3.007.png)

- The CICS IA tree view should show all the CICS profiles created in CICS Extension

    ![](https://github.com/IBM/cics-ia-vs-code-extension/raw/HEAD/docs/images/CICSIA.Words.2521e191-aa0c-43da-8799-3d24aab9b5d3.008.png)

*NOTE: If the CICS connection is failing with red indicator icon then that CICS profile should fail in the CICS IA view also.

![](https://github.com/IBM/cics-ia-vs-code-extension/raw/HEAD/docs/images/CICSIA.Words.2521e191-aa0c-43da-8799-3d24aab9b5d3.009.png)

## Create or Update CICS IA Profile 

1. In Zowe Explorer, expand the CICS IA view and select the ‘+’ button in the existing CICS profile.
2. Select Manage CICS IA Profile.

    ![](https://github.com/IBM/cics-ia-vs-code-extension/raw/HEAD/docs/images/manage_profiles.png)

3. Select Create or Update CICS IA Profile.

    ![](https://github.com/IBM/cics-ia-vs-code-extension/raw/HEAD/docs/images/create_delete_profile.png)

4. Add a new cicsia profile type within the profile section in a team configuration file (zowe.config.json). 
Below is the example:

    ```json
    {
    "cicsia_example": {
        "type": "cicsia",
        "properties": {
        "db2HostName": "replace-with-db2-host-name",
        "db2Location": "replace-with-db2-location",
        "db2PortNumber": "replace-with-db2-port-number",
        "iaApiHostName": "replace-with-ia-rest-api-host-name",
        "iaApiPortNumber": "replace-with-ia-rest-api-port-number",
        "schema": "replace-with-db2-schema-name",
        "name": "replace-with-existing-cics-profile",
        "user": "replace-with-db2-username",
        "password": "replace-with-db2-password",
        "rejectUnauthorized": true
        }
    }
    }

5. After you create a CICS IA profile, the CICS IA view will automatically begin loading data.

    ![](https://github.com/IBM/cics-ia-vs-code-extension/raw/HEAD/docs/images/profile_home_page.png)

## Delete CICS IA Profile 

In Zowe Explorer, expand the CICS IA view and select the ‘+’ button in the existing CICS profile.
- Select Manage CICS IA Profile.
- Select Delete CICS IA Profile to open the configuration file.

    ![](https://github.com/IBM/cics-ia-vs-code-extension/raw/HEAD/docs/images/delete_profile.png)

- Edit the configuration file to remove the CICS IA profile entry.

- Once the CICS IA profile is updated or deleted, again CICS IA view will start loading the data from the DB Schema and refreshes the tree hierarchy inside the updated CICS IA Profile.

## CICS IA Collector View

A new "**CICS IA COLLECTOR**" view will provide a hierarchical representation of your configured collectors and the CICS regions they monitor.

**Connecting using CICS IA Collector Profiles**

Similar to CICS IA and CICS profiles, CICS IA Collector profiles are stored with other Zowe profiles in team configuration JSON files.

CICS IA collector profiles inherit properties from base profiles in the same way as Zowe profiles. Credentials are securely stored using the Zowe profile mechanism, with secure arrays and autoStore.

<a name="_hlk208418687"></a>**Create or Update the CICS IA Profile**

Execute the steps below to create or update the CICS IA Profile:

1. In Zowe Explorer, select the ‘**+’** button in the CICS IA Collector tree.
1. Select **Create a CICS IA Collector.**

![](https://github.com/IBM/cics-ia-vs-code-extension/raw/HEAD/docs/images/Aspose.Words.ca144599-db0d-4633-863a-bc5ad6a9731e.001.png)

1. Select <a name="_hlk208418947"></a>**Create a New Team Configuration File** or **Edit Team Configuration File** to create a new CICS IA Collector profile.

![](https://github.com/IBM/cics-ia-vs-code-extension/raw/HEAD/docs/images/Aspose.Words.ca144599-db0d-4633-863a-bc5ad6a9731e.002.png)

1. Add a new cicsiacollector profile type to the profile section of a team configuration file (zowe.config.json).\
\
   **Example:** The following example shows a CICS IA Collector profile stored in a configuration file. The host, port, and protocol in a CICS profile must point to a valid CICS IA Collector connection:

    ```json
    {
        "collector121": {
            "type": "cicsiacollector",
            "properties": {
                "name": "collector121",
                "collectorHostName": "xxx.xxx.xxx.com",
                "collectorPortNumber": "xxx",
                "iaSecureConnection": false,
                "user": "IATEST",
                "password": "MJU00YHN",
                "rejectUnauthorized": false
            }
        }
    }
    ```

1. After creating the CICS IA Collector profile, the CICS IA Collector view will automatically begin loading the data. 

    ![](https://github.com/IBM/cics-ia-vs-code-extension/raw/HEAD/docs/images/Aspose.Words.ca144599-db0d-4633-863a-bc5ad6a9731e.003.png)

   **Note:** It uses the connection details you provided in the profile to connect to the CICS collector.


**Deleting CICS IA Collector Profile**

1. In Zowe Explorer, right-click on the required CICS IA Collector profile.
1. Select **Manage profile.**

    ![](https://github.com/IBM/cics-ia-vs-code-extension/raw/HEAD/docs/images/Aspose.Words.ca144599-db0d-4633-863a-bc5ad6a9731e.004.png)


1. Select **Delete CICS IA Collector Profile.**

   ![](https://github.com/IBM/cics-ia-vs-code-extension/raw/HEAD/docs/images/Aspose.Words.ca144599-db0d-4633-863a-bc5ad6a9731e.005.png)

1. Edit the configuration file to remove the CICS IA Collector profile entry.

**Manage CICS IA Collector**

The **Manage CICS IA Collector** feature provides essential options to control and monitor the data collection process for a selected CICS region. When you right-click on a specific region (for example, *C63C3C08*), a context menu displays the following options:

![](https://github.com/IBM/cics-ia-vs-code-extension/raw/HEAD/docs/images/Aspose.Words.ca144599-db0d-4633-863a-bc5ad6a9731e.006.png)


**Continue Collector**: This command is used to resume a collection session that was previously paused.

**Pause Collector**: This option temporarily suspends data collection. It's useful for stopping monitoring without ending the session, for example, during a maintenance window.

**Start Collector**: Use this to begin a new data collection session for an inactive region. The collector will start monitoring transactions and resource access.

**Stop Collector**: This command completely ends the current collection session. The collected data is finalized and stored, ready for analysis.

## CICS IA Profile
CICS IA profile upon successful connection displays Green indicator icon over the profile name. If connection not successful, then displays Red indicator icon over the profile name. CICS IA profile on Successful connection extracts the Collected Dependency and Affinity data from the DB2 Schema to which REST API is configured. When CICS IA profile node is expanded, below child items are listed.

**Collection IDs:** Collected data has been grouped under Collection IDs and is used for analysing the collected data. For more information, See [Collection IDs.](#collection-ids)

**User Command Flow:** Displays the Command flow runs sorted by User ID. For more information, See [User Command Flow.](#user-command-flow)

**Reports:** Displays the Threadsafe reports which have been generated for a Region, Program or transaction. For more information, See [Reports](#reports).

![](https://github.com/IBM/cics-ia-vs-code-extension/raw/HEAD/docs/images/CICSIA.Words.2521e191-aa0c-43da-8799-3d24aab9b5d3.014.png)
## Collection IDs 
The Collection IDs are the collection identifiers for which dependency or affinity data has been collected by CICS IA tool and loaded into DB2. 

Hover over the Side bar and expand the CICS IA profile node. List of Collection ID tree items would be displayed under the CICS IA profile tree node. Select the Collection ID that you want to explore. 

![](https://github.com/IBM/cics-ia-vs-code-extension/raw/HEAD/docs/images/CICSIA.Words.2521e191-aa0c-43da-8799-3d24aab9b5d3.015.png)

On expanding a desired collection ID tree node, **four** child items – Regions, Web Services, Transactions, Programs will be displayed for the selected collection ID.

![](https://github.com/IBM/cics-ia-vs-code-extension/raw/HEAD/docs/images/CICSIA.Words.2521e191-aa0c-43da-8799-3d24aab9b5d3.016.png)

- **Regions View:** Lists the CICS regions for which data has been collected under the selected Collection ID. For more information, see [REGIONS](#regions).
- **Web services view:** Lists the web services known to the selected Collection ID.** For more information, see [WEB SERVICES](#webservices)
- **Transactions view:** Lists the Transactions known to the selected Collection ID.** For more information, see [TRANSACTIONS](#transactions).
- **Programs View:** Lists the Programs known to the selected Collection ID.** For more information, see [PROGRAMS](#programs).
## Regions
CICS® region information that is collected by CICS IA is displayed when you expand **Regions** node under a Collection ID. Next to Regions text within brackets, a count of the regions used in the selected collection ID is displayed. 

![](https://github.com/IBM/cics-ia-vs-code-extension/raw/HEAD/docs/images/CICSIA.Words.2521e191-aa0c-43da-8799-3d24aab9b5d3.017.png)
## Regions Menu
Expand **Regions** node**.** Right-click the region that you want to explore and choose an option from the menu. Use the menu to display more information about the selected region. 

The following menu options are available:

- **Show Resources**. Displays all the resources for the selected region in the [Show Resources view](#threadsafe-report-view) "The Show Resources view displays resources from a number of sources, including searches run from the toolbar, from the Queries view, and from the Regions view.".
- **Show Maps**. Displays the MAP resource types for the selected region in the [Show Resources view](#threadsafe-report-view) "The Show Resources view displays resources from a number of sources, including searches run from the toolbar, from the Queries view, and from the Regions view.".
- **Show Files**. Displays the FILE resource types for the selected region in the [Show Resources view](#threadsafe-report-view) "The Show Resources view displays resources from a number of sources, including searches run from the toolbar, from the Queries view, and from the Regions view.".
- **Show Temporary Storage**. Displays the TSQUEUE resource types for the selected region in the [Show Resources view](#threadsafe-report-view) "The Show Resources view displays resources from a number of sources, including searches run from the toolbar, from the Queries view, and from the Regions view.".
- **Show Transient Data**. Displays the TDQUEUE resource types for the selected region in the [Show Resources view](#threadsafe-report-view) "The Show Resources view displays resources from a number of sources, including searches run from the toolbar, from the Queries view, and from the Regions view.".
- **Program for API enablement.** Displays programs that don't have presentation logic and are suitable candidates for being exposed as an API for the selected region in the [Show Resources view](#threadsafe-report-view) "The Show Resources view displays resources from a number of sources, including searches run from the toolbar, from the Queries view, and from the Regions view.".
- **Report** > **Threadsafe Report**. Create a report of threadsafe issues for the programs in the selected region and display report in the [Reports](#reports) "To create affinity reports, and build files of CICSPlex SM Workload Manager (WLM) transaction groups for input to CICSPlex SM expand Reports in the IA Navigation view. You can also manage saved affinity reports, threadsafe reports, and transaction group files ". You can select whether to generate report across all regions or a specific region. To generate report across all regions, click All Regions in the submenu. To generate report across a specific region, click Specific Region from the submenu, then select the required CICS region from the list displayed below the search bar.
- **Report** > **Affinity Report**.. Create an affinity report for the regions you require and display the report in the [Reports](#reports)."You can select whether to generate report across all regions or a specific region. To generate report across all regions, select the regions that you require a report for and the affinity types that you require in the report.".
- **Transactions Used**. Filters and Displays the transactions that are used in the selected region in the [Transactions](#transactions) node. And region for which Transactions are filtered is appended to the Transaction Node. To remove this filter, Click on the Resource filter icon ![](https://github.com/IBM/cics-ia-vs-code-extension/raw/HEAD/docs/images/CICSIA.Words.2521e191-aa0c-43da-8799-3d24aab9b5d3.018.png) displayed at the end of Transaction node. 

  ![](https://github.com/IBM/cics-ia-vs-code-extension/raw/HEAD/docs/images/CICSIA.Words.2521e191-aa0c-43da-8799-3d24aab9b5d3.019.png)

- **Programs Used**. Filters and Displays the programs that are used in the selected region in the [Programs](#programs) "The Programs view shows an alphabetical list of all programs known to CICS IA." Node. And region for which Programs are filtered is appended to the Program Node. To remove this filter, Click on the Resource filter icon ![](https://github.com/IBM/cics-ia-vs-code-extension/raw/HEAD/docs/images/CICSIA.Words.2521e191-aa0c-43da-8799-3d24aab9b5d3.018.png) displayed at the end of Program node.

  ![](https://github.com/IBM/cics-ia-vs-code-extension/raw/HEAD/docs/images/CICSIA.Words.2521e191-aa0c-43da-8799-3d24aab9b5d3.020.png)

- **Web Services Used**. Filters and Displays the web services that are used in the selected region in the [Web Services](#webservices) "The Web Services view displays an alphabetic list of all web services known to CICS IA, both inbound and outbound." node. And region for which Web Services are filtered is appended to the Web Service Node. To remove this filter, Click on the Resource filter icon ![](https://github.com/IBM/cics-ia-vs-code-extension/raw/HEAD/docs/images/CICSIA.Words.2521e191-aa0c-43da-8799-3d24aab9b5d3.018.png)displayed at the end of Web Services node.

![](https://github.com/IBM/cics-ia-vs-code-extension/raw/HEAD/docs/images/CICSIA.Words.2521e191-aa0c-43da-8799-3d24aab9b5d3.021.png)

- **Show Affinities by Type**. Select an affinity group type from the submenu to display the resources for the selected region that have potential affinities in the Affinities view.

- **Visualization**. Display the programs and transactions in the selected region as groups in the Resource Usage Visualization view.

## Webservices 
The Web Services node displays an alphabetic list of all web services known to CICS® IA Collection ID, both inbound and outbound. Next to Web Services text within brackets, a count of the web services used in the selected collection ID is displayed.

Right-click the web service that you want to analyze to see the resources that it uses and where it is used, either across all regions or for a specific region. 

For an inbound web service, you can see the resources that it uses. For an outbound web service, you can see where it was invoked by transaction or program.

![](https://github.com/IBM/cics-ia-vs-code-extension/raw/HEAD/docs/images/CICSIA.Words.2521e191-aa0c-43da-8799-3d24aab9b5d3.022.png)
## Webservices Menu
Expand **Web Services** node**.** Right-click the web service that you want to explore and choose an option from the menu. Use the menu to display more information about the selected webservice. 

The following menu options are available:

- **Used by applications.** Displays the applications where selected web service is being used. The results are shown in the [Show Resources view](#threadsafe-report-view) "The Show Resources view displays resources from a number of sources, including searches run from the toolbar, from the Queries view, and from the Regions view.". You can select whether to search across all platforms or a specific platform. To search across all platforms, click All Platforms from Sub Menu. To search across a specific platform, click Specific Platform from Sub Menu, then select the required platform displayed below the search bar.
- **Used by Programs.** Displays the programs where selected web service is being used. The results are shown in the [Used By View.](#used-by-view) "The Show Resources view displays resources from a number of sources, including searches run from the toolbar, from the Queries view, and from the Regions view." You can select whether to search across all regions or a specific region. To search across all regions, click All Regions in the submenu. To search across a specific region, click Specific Region from the submenu, then select the required CICS region from the list displayed below the search bar.
- **Used by Transactions.** Displays the transactions where selected web service is being used. The results are shown in the [Used By View.](#used-by-view) "The Show Resources view displays resources from a number of sources, including searches run from the toolbar, from the Queries view, and from the Regions view." You can select whether to search across all regions or a specific region. To search across all regions, click All Regions in the submenu. To search across a specific region, click Specific Region from the submenu, then select the required CICS region from the list displayed below the search bar.
- **Used by Region.** Displays the regions where selected web service is being used. The results are shown in the [Show Resources view](#threadsafe-report-view) "The Show Resources view displays resources from a number of sources, including searches run from the toolbar, from the Queries view, and from the Regions view.". 
- **Uses Resources**. Display all the resources used by the selected web Service in the [Uses view](#uses-view) "The Show Resources view displays resources from a number of sources, including searches run from the toolbar, from the Queries view, and from the Regions view.". You can select whether to search across all regions or a specific region. To search across all regions, click All Regions in the submenu. To search across a specific region, click Specific Region from the submenu, then select the required CICS region from the list displayed below the search bar.

![](https://github.com/IBM/cics-ia-vs-code-extension/raw/HEAD/docs/images/CICSIA.Words.2521e191-aa0c-43da-8799-3d24aab9b5d3.023.png)
## Transactions
The Transactions Node shows an alphabetical list of all transactions known to CICS® IA Collection ID. Next to Transactions text within brackets, a count of the transactions used in the selected collection ID is displayed.

The list of transactions includes the transactions in which programs are running and transactions that are the results of interactions; that is, they are CICS resources of type TRANSID.

![](https://github.com/IBM/cics-ia-vs-code-extension/raw/HEAD/docs/images/transaction_menus.png)
## Transactions Menu
Expand **Transactions** node**.** Right-click the Transaction that you want to explore and choose an option from the menu. Use the menu to display more information about the selected Transaction. 

The following menu options are available:

- **Used by applications.** Displays the applications where selected Transaction is being used. The results are shown in the [Show Resources view](#show-resources-view) "The Show Resources view displays resources from a number of sources, including searches run from the toolbar, from the Queries view, and from the Regions view.". You can select whether to search across all platforms or a specific platform. To search across all platforms, click All Platforms from Sub Menu. To search across a specific platform, click Specific Platform from Sub Menu, then select the required platform from the list displayed below the search bar. 
- **Used by Programs.** Displays the programs where selected Transaction is being used. The results are shown in the [Used By View.](#used-by-view) "The Show Resources view displays resources from a number of sources, including searches run from the toolbar, from the Queries view, and from the Regions view." You can select whether to search across all regions or a specific region. To search across all regions, click All Regions in the submenu. To search across a specific region, click Specific Region from the submenu, then select the required CICS region from the list displayed below the search bar.
- **Used by Transactions.** Displays the transactions where selected Transaction is being used. The results are shown in the [Used By View.](#used-by-view) "The Show Resources view displays resources from a number of sources, including searches run from the toolbar, from the Queries view, and from the Regions view." You can select whether to search across all regions or a specific region. To search across all regions, click All Regions in the submenu. To search across a specific region, click Specific Region from the submenu, then select the required CICS region from the list displayed below the search bar.
- **Used by Region.** Displays the regions where selected Transaction is being used. The results are shown in the [Show Resources view](#show-resources-view) "The Show Resources view displays resources from a number of sources, including searches run from the toolbar, from the Queries view, and from the Regions view.". 
- **Uses Resources**. Displays all the resources used by the selected Transaction in the [Uses view](#uses-view) "The Show Resources view displays resources from a number of sources, including searches run from the toolbar, from the Queries view, and from the Regions view.". You can select whether to search across all regions or a specific region. To search across all regions, click All Regions in the submenu. To search across a specific region, click Specific Region from the submenu, then select the required CICS region from the list displayed below the search bar.
- **Show Tasks**. Displays all the tasks in the selected Transaction. The results are shown in the [Show Resources view](#show-resources-view) "The Show Resources view displays resources from a number of sources, including searches run from the toolbar, from the Queries view, and from the Regions view.". 
- **Show Affinities By Type.** Select an affinity group type from the submenu to display the resources for the selected Transaction that have potential affinities in the [Affinities view].
- **Threadsafe Report.** Used to create a report of threadsafe issues for the selected Transaction. Threadsafe report will be saved under the REPORTS section of CICS IA profile. You can select whether to generate report across all regions or a specific region. To generate report across all regions, click All Regions in the submenu. To generate across a specific region, click Specific Region from the submenu, then select the required CICS region from the list displayed below the search bar. See [Creating a report of threadsafe issues](#creating-a-report-of-threadsafe-issues) for more information.

- **Visualization**. To see a visual representation of programs and transactions as groups, right-click the transaction name then click Visualization. See [Resource Usage Visualization view](#resource-usage-visualization-view).

- **Show Command Flow Runs**. The Show command flow runs feature provides diagnostic insights into the execution flow and resource usage of a specific transaction in the CICS environment.

- **Show Program Flow Path**. The Show Program Flow Path feature, available in cics ia vs code extension Program Flows view, provides a detailed mapping of the sequence of programs executed for a specific transaction in a CICS environment

    ![](https://github.com/IBM/cics-ia-vs-code-extension/raw/HEAD/docs/images/transaction_menus.png)

## Programs
The Programs node shows an alphabetical list of all programs known to CICS® IA Collection ID. Next to Programs text within brackets, a count of the Programs used in selected collection ID is displayed.

The list of Programs include:

- Programs that are the sources of interactions
- Programs that make calls into CICS
- Programs that are the results of interactions
- Programs that are CICS resources of type PROGRAM

![](https://github.com/IBM/cics-ia-vs-code-extension/raw/HEAD/docs/images/CICSIA.Words.2521e191-aa0c-43da-8799-3d24aab9b5d3.026.png)
## Programs Menu
Expand **Programs** node**.** Right-click the Program that you want to explore and choose an option from the menu. Use the menu to display more information about the selected Program. 

The following menu options are available:

- **Used by applications.** Displays the applications where selected Program is being used. The results are shown in the [Show Resources view](#show-resources-view) "The Show Resources view displays resources from a number of sources, including searches run from the toolbar, from the Queries view, and from the Regions view.". You can select whether to search across all regions or a specific region. To search across all regions, click All Regions in the submenu. To search across a specific region, click Specific Region from the submenu, then select the required CICS region from the list displayed below the search bar.
- **Used by Programs.** Displays the programs where selected Program is being used. The results are shown in the [Used By View.](#used-by-view) "The Show Resources view displays resources from a number of sources, including searches run from the toolbar, from the Queries view, and from the Regions view." You can select whether to search across all regions or a specific region. To search across all regions, click All Regions in the submenu. To search across a specific region, click Specific Region from the submenu, then select the required CICS region from the list displayed below the search bar.
- **Used by Transactions.** Displays the transactions where selected Program is being used. The results are shown in the [Used By View.](#used-by-view) "The Show Resources view displays resources from a number of sources, including searches run from the toolbar, from the Queries view, and from the Regions view." You can select whether to search across all regions or a specific region. To search across all regions, click All Regions in the submenu. To search across a specific region, click Specific Region from the submenu, then select the required CICS region from the list displayed below the search bar.
- **Used by Region.** Displays the regions where selected Program is being used. The results are shown in the [Show Resources view](#show-resources-view) "The Show Resources view displays resources from a number of sources, including searches run from the toolbar, from the Queries view, and from the Regions view.". 
- **Uses Resources**. Displays all the resources used by the selected Program in the [Uses view](#uses-view) "The Show Resources view displays resources from a number of sources, including searches run from the toolbar, from the Queries view, and from the Regions view.". You can select whether to search across all regions or a specific region. You can select whether to search across all regions or a specific region. To search across all regions, click All Regions in the submenu. To search across a specific region, click Specific Region from the submenu, then select the required CICS region from the list displayed below the search bar.
- **Show Details**. Displays the properties of the selected Program. The results are shown in the [Program](#program-details-view) "The Show Resources view displays resources from a number of sources, including searches run from the toolbar, from the Queries view, and from the Regions view." Details View. 
- **Show Affinities By Type.** Select an affinity group type from the submenu to display the resources for the selected region that have potential affinities in the [Affinities view].
- **Threadsafe Report.** Used to create a report of threadsafe issues for the selected Program. Threadsafe report will be saved under the REPORTS section of CICS IA profile. You can select whether to generate report across all regions or a specific region. To generate report across all regions, click All Regions in the submenu. To generate across a specific region, click Specific Region from the submenu, then select the required CICS region from the list displayed below the search bar. See [Creating a report of threadsafe issues](#creating-a-report-of-threadsafe-issues) for more information.

- **Visualization**. To see a visual representation of programs and transactions as groups, right-click the transaction name then click Visualization. See [Resource Usage Visualization view](#resource-usage-visualization-view).

    ![](https://github.com/IBM/cics-ia-vs-code-extension/raw/HEAD/docs/images/program_menus.png)

## User Command Flow
When you expand **User Command Flow** Node under CICS IA profile tree Hierarchy, it displays a list of command flow runs which are sorted by user ID. 

Hover over the Side bar and expand the CICS IA profile node. Expand the **USER COMMAND FLOW** node to view the USER IDs for which CICS IA collected command flow data. 

To view a command flow that was run by a user, expand the required user ID. You can then expand the command flow to display further information. The time of the first command that is issued, and the transaction task ID are displayed. Before any transaction or program resource can be visualized from the User Command Flow Execution, interdependency data must first be collected for the transaction and loaded into the DB2 table.

![](https://github.com/IBM/cics-ia-vs-code-extension/raw/HEAD/docs/images/command_flow_visualization.png)
## User Command Flow Menu
Right-click on a transaction task ID and use the following menu options to show more information about a task in a command flow run:

- **Show Execution**. Display the execution details of the selected task in the [Command Flow view](#command-flow-view) "The Command Flow view shows the execution details of a selected task. It shows the Task Control Block (TCB) modes that were used, any TCB mode switches, and a command flow table.".
- **Visualization**. Then, select from below options to display the command flow diagram for the selected transaction in the [Command Flow Diagram view](#command-flow-diagram-view) "The Command Flow Diagram view shows a timeline of the commands that the Command Flow Collector has collected. Commands are grouped by program, then displayed in rows or columns that represent the different platforms and applications, regions, or Task Control B".
  - **Application Switches**. Display the programs in rows or columns that represent the program and applications, with arrows to show the switches.
  - **Region Switches**. Display the programs in rows or columns that represent the regions, with arrows to show the switches.
  - **TCB Switches**. Display the programs in rows or columns that represent the TCBs, with arrows to show the switches.
## Reports
You can expand **Reports node** under CICS IA profile tree Hierarchy for the following functions:

- Open, a saved report or file.

Hover over the Side bar and expand the CICS IA profile. Expand the **REPORTS** node to view saved Threadsafe reports. 

![](https://github.com/IBM/cics-ia-vs-code-extension/raw/HEAD/docs/images/CICSIA.Words.2521e191-aa0c-43da-8799-3d24aab9b5d3.029.png)

## Reports Menu
Use the menus in **Reports** to manage the folders and reports. Right-click the report, or file that you require and choose one of the following options from the menu:

- **Open report**. Open the currently selected report or file in the appropriate view:
  - For a threadsafe report, open the Threadsafe Report view. See [Threadsafe Report view.](#threadsafe-report-view) "Use the Threadsafe Report view to view or create summary or detailed reports of threadsafe issues in HTML format." 
- **Open in Browser**. Open the currently selected threadsafe report in the Report Browser view. See [Report Browser view](#report-browser-view) "Use the Report Browser view to view the contents of saved affinity or threadsafe reports.".

![](https://github.com/IBM/cics-ia-vs-code-extension/raw/HEAD/docs/images/CICSIA.Words.2521e191-aa0c-43da-8799-3d24aab9b5d3.030.png)
## Program details view
The Program Details view shows the properties of a program in CICS® IA.

To see the properties of a program, Select a program displayed under the Programs node. Right-click the program name and click **Show Details**.

Editor Window shows the Program details view with the program name as the title.

This view lists the program attributes, with a column for each region where the program is used. Attributes are organized into groups, and you can expand or collapse those groups.

![](https://github.com/IBM/cics-ia-vs-code-extension/raw/HEAD/docs/images/CICSIA.Words.2521e191-aa0c-43da-8799-3d24aab9b5d3.031.png)
## Show Resources view
The Show Resources view displays resources for a selected Region or Transaction or Program or Web Service.

Resources are organized into a tree structure. The following screen shows the results for MAP resources for selected region.

![](https://github.com/IBM/cics-ia-vs-code-extension/raw/HEAD/docs/images/CICSIA.Words.2521e191-aa0c-43da-8799-3d24aab9b5d3.032.png)

Header of this view displays the region for which resources are displayed. Also displays a count of the selected resource type. 

Below the header, a toolbar is displayed with tools for 

<a name="_used_by_view"></a>	![](https://github.com/IBM/cics-ia-vs-code-extension/raw/HEAD/docs/images/CICSIA.Words.2521e191-aa0c-43da-8799-3d24aab9b5d3.033.png)  Expand all the resources in the view.

![](https://github.com/IBM/cics-ia-vs-code-extension/raw/HEAD/docs/images/CICSIA.Words.2521e191-aa0c-43da-8799-3d24aab9b5d3.034.png) Collapse all resources in the view.

You can recall the results of previous searches, and move between searches, by using the Previous search ![](https://github.com/IBM/cics-ia-vs-code-extension/raw/HEAD/docs/images/CICSIA.Words.2521e191-aa0c-43da-8799-3d24aab9b5d3.035.png) and Next search ![](https://github.com/IBM/cics-ia-vs-code-extension/raw/HEAD/docs/images/CICSIA.Words.2521e191-aa0c-43da-8799-3d24aab9b5d3.036.png)  icons in the toolbar of the view.  

## Resource Usage Visualization View
Use the Resource Usage Visualization view to display a visual representation of programs and transactions as groups.

The Resource Usage Visualization view displays resources as containers that you can expand to show the child resources. It provides an alternative to the Show Resources view, where resources in a region are displayed in a list. 

To open the Resource Usage Visualization view, right-click one of the following resources, then click Visualization:

- Program. 
- Region. After you click Visualization, click one of the following options, as required:
    - By Transactions (All Regions)
    - By Transactions (Selected Region)
    - By CICS TS Applications (All Regions)
    - By CICS TS Applications (Selected Region)

- Transaction.

![](https://github.com/IBM/cics-ia-vs-code-extension/raw/HEAD/docs/images/region_visualization.png)

Each container in the Resource Usage Visualization view has a title with a resource name, an icon that represents the resource, and the number of child resources. By default, the resources are grouped by platforms, and then by applications. If you visualize a region by transactions, or if you are connected to a CICS® IA Version 5.1 or earlier database, the resources are grouped by regions, and then by applications.

- **Toolbar**

- **Swap top level elements** icon ![](https://github.com/IBM/cics-ia-vs-code-extension/raw/HEAD/docs/images/swap_top_level_element.png). Change the current resource grouping. If you are connected to a CICS IA Version 5.2 or later database, change the resource grouping between grouping by applications then by platforms, and grouping by platforms then by applications. For visualization of a region by transactions, or if you are connected to an earlier version database, change the resource grouping between grouping by applications then by regions, and grouping by regions then by applications.
- **Collapse all** icon ![](https://github.com/IBM/cics-ia-vs-code-extension/raw/HEAD/docs/images/collapse_all.png). Collapse all the containers to the top level containers.
- **Expand all** icon ![](https://github.com/IBM/cics-ia-vs-code-extension/raw/HEAD/docs/images/expand_all.png). Expand all the containers in the editor.

## Comparision of Resources
The Comparison of CICS Resources feature within CICS IA now enables users to compare resources utilized by transactions across different or the same Collector IDs for a CICS application. This includes resources such as Programs, Transactions, Mapsets, Conditions, and Texts. The implementation displays all fetched resources in a CICS IA Comparison of CICS Resource view, presenting differences side by side in a VS Code extension interface for efficient analysis.

Follow the steps below to compare the CICS resources:
- Navigate to the CICS IA view.
- Right-click on the required CICS IA profile node (e.g., hclctc3) and     select Compare CICS Resources.

![](https://github.com/IBM/cics-ia-vs-code-extension/raw/HEAD/docs/images/comparision_of_res_01.png)

- The Comparison of CICS Resources view will open in the right-side panel.

- Enter the Region ID, Collector ID, and Transaction ID for the Source and Target and select Continue.

![](https://github.com/IBM/cics-ia-vs-code-extension/raw/HEAD/docs/images/comparision_of_res_02.png)

**Note:** You cannot compare identical configurations. The system checks for identical configurations. If all fields match, an error message ("You cannot compare the same transaction under the same collection ID") is displayed and disables the Continue button.

![](https://github.com/IBM/cics-ia-vs-code-extension/raw/HEAD/docs/images/comparision_of_res_03.png)

- Use Reset to clear fields.

- It starts collecting data, and the resources linked to the chosen transactions are displayed in separate views, as illustrated below.
![](https://github.com/IBM/cics-ia-vs-code-extension/raw/HEAD/docs/images/comparision_of_res_04.png)

The difference in the resources for the selected transactions is highlighted in a different color (RED) for better understanding, as shown in the image below.  

![](https://github.com/IBM/cics-ia-vs-code-extension/raw/HEAD/docs/images/comparision_of_res_05.png)

When the user selects Show similar resource toolbar, it filters the similar resource contents between the transactions, as shown in the image below.

![](https://github.com/IBM/cics-ia-vs-code-extension/raw/HEAD/docs/images/comparision_of_res_06.png)

When the user selects the Show All resource toolbar, the filter is cleared, and the contents of all resources between the transactions are shown in the image below.

![](https://github.com/IBM/cics-ia-vs-code-extension/raw/HEAD/docs/images/comparision_of_res_07.png)

## Program Flow Editor
You can create a report of grouped program flows of a CICS TS Transaction that was collected by the Command Flow Collector.

Users can display the Program flow editor by Right-click on a transaction and select Show program flow paths.

![](https://github.com/IBM/cics-ia-vs-code-extension/raw/HEAD/docs/images/pflow01.png)

There are three fields in the Program Flows editor. Customize the fields to generate the report. 

![](/docs/images/pflow02.png)

- **Command Flow ID** : This field defines the Command Flow ID for root tasks. You can use a fixed value or * (All) wildcards.
- **Initial Region** : This field defines the initial region for root tasks. You can use a fixed value or * (All) wildcards.
- **Transaction ID** : The name of the transaction to be investigated. You can only use a fixed value.

Click the **Run** button to the right of the Transaction field to generate the report. The report usually takes some time to generate.

The report is generated and the trees of program flows are displayed. Each item in a tree is called a node. There are two types of nodes: transaction and program nodes. If the nodes of any two trees have the same types, same orders, and same names, the two trees are put into the same group. Otherwise, the trees are divided into different groups. 

The number to the right of the root program of a group shows the count of trees in this group. Nodes in a tree are sorted by execution time.


## Used By view
From Region, transaction or program or web service node where a resource is available, you can view the programs or the transactions or the web service that are using the resource and the associated regions. 

Use the Used By menu options to show the regions in which the program or transaction is being used. You can analyze the use of each program or transaction or web service across all regions or specific regions.

![](https://github.com/IBM/cics-ia-vs-code-extension/raw/HEAD/docs/images/CICSIA.Words.2521e191-aa0c-43da-8799-3d24aab9b5d3.037.png)

If you select one of the options in the Used By menu, information is displayed in the Used By view:

![](https://github.com/IBM/cics-ia-vs-code-extension/raw/HEAD/docs/images/CICSIA.Words.2521e191-aa0c-43da-8799-3d24aab9b5d3.038.png)

The use tree of the resource is shown in the Used By view. The previous screen capture shows the uses of the program HCLMENU1.

Header of this view displays the resource currently being analyzed and whether analysis is for all regions or for a specific region. Header also provides a count of resources (Program/Transaction) using selected Program/Transaction/Webservice.

Below the header, a toolbar is displayed with tools for 

`      `![](https://github.com/IBM/cics-ia-vs-code-extension/raw/HEAD/docs/images/CICSIA.Words.2521e191-aa0c-43da-8799-3d24aab9b5d3.039.png)  Expand all the resources in the view.

![](https://github.com/IBM/cics-ia-vs-code-extension/raw/HEAD/docs/images/CICSIA.Words.2521e191-aa0c-43da-8799-3d24aab9b5d3.040.png) Collapse all resources in the view.

You can recall the results of previous searches, and move between searches, by using the Previous search ![](https://github.com/IBM/cics-ia-vs-code-extension/raw/HEAD/docs/images/CICSIA.Words.2521e191-aa0c-43da-8799-3d24aab9b5d3.041.png) and Next search ![](https://github.com/IBM/cics-ia-vs-code-extension/raw/HEAD/docs/images/CICSIA.Words.2521e191-aa0c-43da-8799-3d24aab9b5d3.042.png)  icons in the toolbar of the view.  
## Uses view
From transaction or program or web service node, you can explore resources further to see which resources the transaction or program or webservice is using and in which regions. 

To show the regions in which the program or transaction or webservice resource is being used, right-click the resource, then click Uses Resources. You can specify whether to analyze use for a specific region, or for all regions.

The information about the selected resource and region populates the Uses view in the Editor window.

Select **Uses Resources > Specific Region** to display the resources used in that region.

![](https://github.com/IBM/cics-ia-vs-code-extension/raw/HEAD/docs/images/CICSIA.Words.2521e191-aa0c-43da-8799-3d24aab9b5d3.043.png)

The Uses view has three sections:

- The Left Pane displays the list of resources used by selected Program/Transaction/Webservice organized into folders by **Resource Type**. If you expand a resource Type folder by clicking ![](https://github.com/IBM/cics-ia-vs-code-extension/raw/HEAD/docs/images/CICSIA.Words.2521e191-aa0c-43da-8799-3d24aab9b5d3.044.png), you can view the resources using the specific resource type. If we expand resource further by clicking ![](https://github.com/IBM/cics-ia-vs-code-extension/raw/HEAD/docs/images/CICSIA.Words.2521e191-aa0c-43da-8799-3d24aab9b5d3.044.png),, you can view the verb nodes that were executed against the resource.
  - In the above example on expanding Program Resource Type folder, we get to see 2 Programs TESTPGM and TESTPGM2. On expanding TESTPGM2 resource, we could see that the program TESTPGM2 resource was executed using 2 commands LINK and LOAD.
- The Middle Pane displays Program/Transaction in which the selected resource is invoked.
- The right Pane displays tree hierarchy for the resource usage grouped by Regions.

## Affinities view
The Affinities view displays an alphabetical list of resources with potential affinities related to the target object.

CICS® transactions and programs use some techniques to exchange data that require those transactions or programs to run in the same CICS region, or in a specific CICS region. The result of such requirements is restrictions on the regions to which transactions and distributed program link (DPL) requests can be dynamically routed. If transactions or programs exchange data in ways that impose such restrictions, these are known as affinities between them.

The affinity-related functions of CICS IA have the following uses:

- Users of CICS dynamic routing can determine whether any transactions in their CICS applications have an inter-transaction affinity (some transactions must run in the same region) or a transaction-system affinity (some transactions must run in a specific region).
- Application programmers can detect whether a program being developed might cause transaction affinities.

![](https://github.com/IBM/cics-ia-vs-code-extension/raw/HEAD/docs/images/CICSIA.Words.2521e191-aa0c-43da-8799-3d24aab9b5d3.045.png)

Right-click the item that you want to view the affinities for and click **Show Affinities By Type**. The **Show Affinities By Type** menu is linked to the type of object that is currently selected, rather than the view the object is in. You can also right-click an item in the Programs or Transactions node to display the affinities menu items.

The Affinities view includes 2 sections. 

- The upper section displays either,
  - Affinity Group or 
  - Resource, the affinity relation type, Lifetime of affinity or
  - Affinity relation type, Lifetime of affinity
- Upon selection of an item in the upper section, the lower section displays the Transaction, Program and Command resulting in the selected affinity type.

## Affinities Report view
Use the Affinity Report view to view the contents of an affinity report. When you create an affinity report, it is displayed in the Affinity Report view. see [Creating an affinity report](#creating-a-report-of-threadsafe-issues). 

If you use the Create Affinity Report wizard to create more than one affinity report, the first report is displayed in the Affinity Report view, and the additional report files are saved in the Report Explorer view.

To view a saved report in the Affinity Report view, start from the Report Explorer view. Either double-click the report name, or right-click the report name, then click Open report.

The Overview tab shows the region that the report was generated for, the date and time of the report, the report description, and the affinities that were found.

The Transaction Groups tab shows the transaction group definitions that can be built into a CICSPlex® SM Workload Manager (WLM) transaction group file that can be deployed to CICSPlex SM.

The following figures show an example of an affinity report.

![](https://github.com/IBM/cics-ia-vs-code-extension/raw/HEAD/docs/images/affinity_report_overview.png)

TRANSACTION GROUP

![](https://github.com/IBM/cics-ia-vs-code-extension/raw/HEAD/docs/images/affinity_report_transaction_group.png)

## Threadsafe Report view
Use the Threadsafe Report view to view summary or detailed reports of threadsafe issues in HTML format.

For information about creating threadsafe reports, see [Creating a report of threadsafe issues](#creating-a-report-of-threadsafe-issues).

The Threadsafe Report view includes the following sections:

- Program summary section.
- Program details section.
## Program Summary
The upper section of the Threadsafe Report view displays the program summary information. The programs are grouped by the collection IDs and regions. You can expand the tree structure to display the programs and statistics for threadsafe, non threadsafe, indeterminate threadsafe, threadsafe inhibitor, and other calls issued by each program. To show program details, click the program name.

In the **Reentrant** column, Y indicates that the program is reentrant, a blank indicates that the program is not reentrant, and ? indicates that the reentrant status is not known.

![](https://github.com/IBM/cics-ia-vs-code-extension/raw/HEAD/docs/images/CICSIA.Words.2521e191-aa0c-43da-8799-3d24aab9b5d3.046.png)
## Program Details
The lower section of the Threadsafe Report view displays detailed information about each command for the currently selected program in the report summary. This view displays the Command Type, Function, Resource Type, Object, Offset at which the command is located, Use count for the command, Threadsafe status, threadsafe inhibitor status for each command in the selected program.

![](https://github.com/IBM/cics-ia-vs-code-extension/raw/HEAD/docs/images/CICSIA.Words.2521e191-aa0c-43da-8799-3d24aab9b5d3.047.png)
## Command Flow view 
The Command Flow view shows the execution details of a selected task. It shows the Task Control Block (TCB) modes that were used, any TCB mode switches, and a command flow table.")
The Command Flow view shows the execution details of a selected task. It shows the Task Control Block (TCB) modes that were used, any TCB mode switches, and a command flow table.

The Command Flow view has three sections: TCB Modes Used, TCB Mode Switches, and the command flow table.
## TCB Modes Used
The TCB Modes Used section displays a summary of the TCB modes that were used during the execution of the task, including the total number of commands issued in each TCB mode.

To see the individual commands and resources, expand the tree structure.

If you select a command in this section, the command is highlighted in the command flow table.
## TCB Mode Switches
The TCB Mode Switches section displays a summary of any TCB mode switches that occurred during the execution of the task. Commands and resources are grouped by the mode that they switched from, then the mode that they switched to.

To see the mode that is switched to, and individual commands and resources, expand the tree structure.

If you select a command in this section, the command is highlighted in the command flow table.
## Command flow table
The command flow table displays the command flows, ordered by time, under the program that ran the command. By default, the current and previous TCB Mode, and the time when the command ran, are shown for each command.

Events associated with EXEC CICS commands are displayed as child nodes of the command in the view. These child nodes are the events that are triggered against a command.

The icon for a resource can have the following icons attached:

- ![asterisk icon](https://github.com/IBM/cics-ia-vs-code-extension/raw/HEAD/docs/images/CICSIA.Words.2521e191-aa0c-43da-8799-3d24aab9b5d3.048.png)Event processing icon. You can create an event binding, to use with event processing, from this resource. This option is available only for resources and API calls that match valid event processing resources. 
- ![conflict icon](https://github.com/IBM/cics-ia-vs-code-extension/raw/HEAD/docs/images/CICSIA.Words.2521e191-aa0c-43da-8799-3d24aab9b5d3.049.png)TCB mode switch icon. The command caused a TCB mode switch to occur.
- ![warning icon](https://github.com/IBM/cics-ia-vs-code-extension/raw/HEAD/docs/images/CICSIA.Words.2521e191-aa0c-43da-8799-3d24aab9b5d3.050.png)Warning icon. The command has a nonzero RESP or RESP2 code. 

![](https://github.com/IBM/cics-ia-vs-code-extension/raw/HEAD/docs/images/CICSIA.Words.2521e191-aa0c-43da-8799-3d24aab9b5d3.051.png)
## Command Flow Diagram view
The Command Flow Diagram view shows a timeline of the commands that the Command Flow Collector has collected. Commands are grouped by program, then displayed in rows or columns that represent the different platforms and applications, regions, or Task Control Block (TCB) modes that were used.

The Command Flow Diagram view shows all the commands that the Command Flow Collector has collected. Commands are grouped by program, then displayed both chronologically and in rows or columns that represent the different platforms and applications, regions, or Task Control Block (TCB) modes that were used. Application, Region, or TCB mode switches are shown by arrows.

By default, the different platforms and applications, regions, or Task Control Block (TCB) modes that were used are shown in rows. To show this use in columns, use the **Vertical Orientation** ![](https://github.com/IBM/cics-ia-vs-code-extension/raw/HEAD/docs/images/CICSIA.Words.2521e191-aa0c-43da-8799-3d24aab9b5d3.052.png) icon in the toolbar of the view. When in Vertical orientation to show this use in rows, use the **Horizontal Orientation** ![](https://github.com/IBM/cics-ia-vs-code-extension/raw/HEAD/docs/images/CICSIA.Words.2521e191-aa0c-43da-8799-3d24aab9b5d3.053.png) icon in the toolbar of the view.

The following example is a command flow diagram in horizontal orientation that shows Application/ Platform switches.

![](https://github.com/IBM/cics-ia-vs-code-extension/raw/HEAD/docs/images/CICSIA.Words.2521e191-aa0c-43da-8799-3d24aab9b5d3.054.png)

The following example is a command flow diagram in vertical orientation that shows platform and application switches.

![](https://github.com/IBM/cics-ia-vs-code-extension/raw/HEAD/docs/images/CICSIA.Words.2521e191-aa0c-43da-8799-3d24aab9b5d3.055.png)
## Report Browser view 
Use the Report Browser view to view the contents of saved affinity and threadsafe reports.

To view a saved report in the Report Browser view, start from the Report node under CICS IA Profile.

Hover Over the side bar and expand the CICS IA profile.

Expand the REPORTS Node. 

Navigate to the folder where the saved Affinity or Threadsafe report exists.

Right click a threadsafe or affinity report and select **Open Report in Browser**.

For information about creating reports, see [Creating a report of threadsafe issues](#creating-a-report-of-threadsafe-issues "You can create summary or detailed reports of threadsafe issues in HTML format. To create a threadsafe report, you can use a view that shows the region, program, or transaction for which you require a report, or you can use the Report view."). 

see [Creating an affinity report](#creating-an-affinity-report "You can create detailed affinity reports in HTML format"). 

The following figure shows part of an example threadsafe report in the Report Browser view.

![](https://github.com/IBM/cics-ia-vs-code-extension/raw/HEAD/docs/images/CICSIA.Words.2521e191-aa0c-43da-8799-3d24aab9b5d3.056.png)

The following figure shows part of an example affinity report in the Report Browser view
![](https://github.com/IBM/cics-ia-vs-code-extension/raw/HEAD/docs/images/affinity_report_in_browser.png)

## Creating a report of threadsafe issues
You can create summary or detailed reports of threadsafe issues in HTML format. To create a threadsafe report, you can use a region, program, or transaction for which you require a report.

To generate a report of threadsafe issues for a region, program, or transaction, you can select the required region, program, or transaction, then request a report for the selected region, program, or transaction. The report can then be opened from the Reports node.

## ThreadSafe Report Procedure

1. To create a report for a specified region from the Regions Node, Expand the Collection ID and then Regions Node, right-click the region for which you want a threadsafe report, then click **Report** > **Threadsafe Report**. 

![](https://github.com/IBM/cics-ia-vs-code-extension/raw/HEAD/docs/images/create_threadsafe_report_wizard.png)

1. To create a report for a specified program or transaction, use the following procedure:
   1. Expand the Collection ID and then the program or transaction node, right-click the program or transaction for which you want a threadsafe report and click **Threadsafe report**.
   1. To generate a report for all regions, click **All Regions**. To generate report for a specific region, click **Specific Region**, select the required region from the list displayed under search bar

`                                   `![](https://github.com/IBM/cics-ia-vs-code-extension/raw/HEAD/docs/images/CICSIA.Words.2521e191-aa0c-43da-8799-3d24aab9b5d3.058.png)

![](https://github.com/IBM/cics-ia-vs-code-extension/raw/HEAD/docs/images/CICSIA.Words.2521e191-aa0c-43da-8799-3d24aab9b5d3.059.png)

The wizard for creating the Threadsafe Report appears. Follow the wizard to create and save the threadsafe report.

1. In the first page of the wizard, provide values to the following fields to define the scope of the report.
      1. **CICS TS level** to report on only the commands that are available in the specified CICS® TS release.
      1. **Collection ID** to report on programs that were collected with the specified collection ID. You can use a single asterisk character (\*) as a wildcard.
      1. **Region** to report on programs that were collected in the specified CICS region. You can use a single asterisk character (\*) as a wildcard. If you set the CICS TS level in this field, the report displays the threadsafe information for programs in regions that are at that CICS release.
      1. **Program** or **Transaction** to report on commands collected for the named program or transaction. You can use a single asterisk character (\*) as a wildcard. 
      1. **Show detailed data** checkbox used to include details information in the threadsafe report. If not checked then summary threadsafe report will be generated.

    ![](https://github.com/IBM/cics-ia-vs-code-extension/raw/HEAD/docs/images/CICSIA.Words.2521e191-aa0c-43da-8799-3d24aab9b5d3.060.png)

2. In the next page, select a folder to store the report, enter a name for the report in the Text box and click on Finish button to generate the report.

    ![](https://github.com/IBM/cics-ia-vs-code-extension/raw/HEAD/docs/images/CICSIA.Words.2521e191-aa0c-43da-8799-3d24aab9b5d3.061.png)

The generated report appears under the REPORTS node of the CICS IA profile. Refer [Reports](#reports) section to know how to view the threadsafe report.





[Affinities view]: https://www.ibm.com/docs/en/SSGMCP_5.3.0/com.ibm.cics.ia.help/topics/concepts/affinities_view.html "The Affinities view displays an alphabetical list of resources with potential affinities related to the target object."
[Creating a report of threadsafe issues]: https://www.ibm.com/docs/en/SSGMCP_5.3.0/com.ibm.cics.ia.help/topics/tasks/using_reports.html "You can create summary or detailed reports of threadsafe issues in HTML format. To create a threadsafe report, you can use a view that shows the region, program, or transaction for which you require a report, or you can use the Report view."

## Creating an Affinity report
You can create an affinity report in XML format for one or more regions, for one or more affinity types. To create an affinity report, you can use the Regions view. 

To create an affinity report, you use the Create Affinity Report wizard. For each region that you select, you create a separate affinity report. 

## Affinity Report Procedure
1. To create a report for a specified region from the Regions Node, Expand the Collection ID and then Regions Node, right-click the region for which you want an affinity report, then click Report > Affinity Report.

    ![](https://github.com/IBM/cics-ia-vs-code-extension/raw/HEAD/docs/images/create_affinity_report_wizard.png)

2. Select the regions that you require a report for, and the affinity types that you require in the report, then click Next. 
The wizard displays the folder structure that is used for saved reports; that is, the folder structure that is used in the Report Explorer view.

    ![](https://github.com/IBM/cics-ia-vs-code-extension/raw/HEAD/docs/images/create_affinity_report_wizard_step1.png)

3. Specify the report location. You can select an existing folder or click New Folder and create a new folder.
4. Enter the report name.
5. To add a timestamp to the report name, select the Append a timestamp when saving check box.

    ![](https://github.com/IBM/cics-ia-vs-code-extension/raw/HEAD/docs/images/create_affinity_report_wizard_step2.png)

6. Optional: To add a report description, click Next then enter the required description.
7. Click Finish. 

    ![](https://github.com/IBM/cics-ia-vs-code-extension/raw/HEAD/docs/images/create_affinity_report_wizard_step3.png)

Report generation begins and a message is displayed in the Status bar. When generation is complete, the report is displayed in the Affinity Report view. The report file is also saved in a folder that shows the region name in the specified location in the Report Explorer view. If you create more than one affinity report, the first report is displayed in the Affinity Report view, and the additional report files are saved in the Report Explorer view