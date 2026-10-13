**Connect Data to Microsoft Sentinel using Data Connectors**
**Lab Overview**

**Objective: Install required Content Hub solutions, configure data connectors (Azure Activity and Microsoft Defender for Cloud), create an analytics rule, and save a workbook to "My workbooks".**

Microsoft Services Used: Microsoft Sentinel, Azure Policy, Microsoft Defender for Cloud, Log Analytics Workspace.

Environment and Prerequisites: Azure subscription, Resource Group RG2, and the lab1-ws Log Analytics workspace with Microsoft Sentinel enabled (from Lab 01).

**Concepts Learned**

Content Hub Solutions: Bundles of data connectors, workbooks, analytics rules, and hunting queries that can be deployed together to solve specific security use cases.

Data Connectors: The mechanisms that ingest security data into Microsoft Sentinel. These can be policy-based (Azure Activity), API-based (Defender for Cloud), or agent-based (Windows Security Events).

Azure Policy Integration: The Azure Activity connector uses Azure Policy to automatically stream subscription-level activity logs to the Log Analytics workspace without requiring manual configuration per resource.

Scheduled Analytics Rules: Rules that run on a defined frequency to detect threats. The lab emphasized configuring the query scheduling to run every 1 hour and only look up data from the last 1 hour.

Workbooks: Interactive dashboards that visualize data. Saving them to "My workbooks" makes them accessible for ongoing monitoring.

**Implementation**

Deployed Content Hub Solutions:

Installed three solutions: Windows Security Events, Azure Activity, and Microsoft Defender for Cloud.

Configured Azure Activity Connector:

Launched the Azure Policy Assignment Wizard.

Scoped the policy to the subscription/RG2.

Selected the lab1-ws workspace as the primary Log Analytics workspace.

Enabled the Create a remediation task checkbox to apply the policy to existing resources.

Configured Microsoft Defender for Cloud Connector:

Opened the Subscription-based Microsoft Defender for Cloud (Legacy) connector.

Set the subscription status to Connected.

Enabled Bi-directional sync.

Created an Analytics Rule:

Created a scheduled rule based on the "Suspicious number of resource creation or deployment activities" template.

Configured the rule frequency to 1 hour and the rule period to 1 hour.

Saved Azure Activity Workbook:

Navigated to the Content Hub, managed the Azure Activity solution, and saved the Azure Activity workbook to My workbooks.

**Validation and Results**

Solutions Installed: The Content Hub confirms 3 solutions are installed (Azure Activity, Microsoft Defender for Cloud, Windows Security Events).

![image_alt](https://github.com/PhenyoMB/sc-500-labs/blob/dc57af7da4bc6a63f89c88f2629c82dd8f09e887/02-/Deploy%20a%20Microsoft%20Sentinel%20Content%20Hub%20Solution.png)

Azure Activity Connector: The Azure Policy assignment was created successfully with the scope set to RG2, the workspace mapped to lab1-ws, and a remediation task created.

![image_alt](https://github.com/PhenyoMB/sc-500-labs/blob/dc57af7da4bc6a63f89c88f2629c82dd8f09e887/02-/Set%20up%20The%20Data%20Connector%20For%20Azure%20Activity.png)

Defender for Cloud Connector: The subscription is successfully connected with Bi-directional sync enabled.

![image_alt](https://github.com/PhenyoMB/sc-500-labs/blob/dc57af7da4bc6a63f89c88f2629c82dd8f09e887/02-/Set%20up%20The%20For%20Defender%20For%20Cloud%20Connector.png)

Analytics Rule: The rule "Suspicious number of resource creation or deployment activities" was created and validated. It is configured to run every 1 hour, looking at the last 1 hour of data, and is enabled to create incidents.

![image_alt](https://github.com/PhenyoMB/sc-500-labs/blob/dc57af7da4bc6a63f89c88f2629c82dd8f09e887/02-/Create%20an%20Analytics%20Rule.png)

![image_alt](https://github.com/PhenyoMB/sc-500-labs/blob/dc57af7da4bc6a63f89c88f2629c82dd8f09e887/02-/Create%20an%20Analytics%20Rule%202.png)

Workbook: The Azure Activity workbook is successfully saved in "My workbooks".

![image_alt](https://github.com/PhenyoMB/sc-500-labs/blob/dc57af7da4bc6a63f89c88f2629c82dd8f09e887/02-/Ensure%20That%20The%20Azure%20Activity%20Workbook%20Is%20Available%20In%20My%20Workbooks.png)
