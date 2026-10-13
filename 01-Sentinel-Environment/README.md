**Configure your Microsoft Sentinel Environment**
**Lab Overview**

**Objective: Deploy a Microsoft Sentinel workspace meeting specific requirements for region, data retention, and role-based access control (RBAC).**

Microsoft Services Used: Microsoft Sentinel, Log Analytics Workspace, Azure RBAC, Azure Portal.

Environment and Prerequisites: Azure subscription, Resource Group RG2, and an existing user Operator1.

**Concepts Learned**

This lab established the foundational architecture for Microsoft Sentinel. Key concepts included:

Log Analytics Workspace vs. Microsoft Sentinel: The Log Analytics workspace is the underlying data repository and billing boundary. Microsoft Sentinel is the security layer deployed on top of it that provides SIEM and SOAR capabilities.

Data Residency and Retention: Configuring the workspace region ensures data residency compliance. Setting the retention period directly impacts cost and the historical depth available for threat hunting and incident investigation.

Role-Based Access Control (RBAC): Assigning roles at the resource group scope ensures users have the necessary permissions to perform their duties without violating the principle of least privilege.

**Implementation**

Created a Log Analytics Workspace:

Provisioned a workspace named lab1-ws in the West US region, within the RG2 resource group.

Deployed Microsoft Sentinel:

Onboarded Microsoft Sentinel to the lab1-ws workspace.

Assigned RBAC Role:

Navigated to the RG2 resource group's Access control (IAM) blade.

Assigned the Microsoft Sentinel Contributor role to the Operator1 user.

Configured Data Retention:

Navigated to the lab1-ws workspace settings under Usage and estimated costs.

Changed the Data Retention period to 180 days.


**Validation and Results**

Workspace Creation: The Log Analytics workspace lab1-ws was successfully deployed and is active in the West US region.

![image_alt](https://github.com/PhenyoMB/sc-500-labs/blob/55d63ea5d0309dd13cc9b488eb859339de33f4eb/01-Sentinel-Environment/Creating%20Log%20Analytics%20Workspace.png)


Sentinel Deployment: Microsoft Sentinel is successfully enabled on the lab1-ws workspace.

![image_alt](https://github.com/PhenyoMB/sc-500-labs/blob/55d63ea5d0309dd13cc9b488eb859339de33f4eb/01-Sentinel-Environment/Deploy%20Sentinel%20To%20A%20Workspace.png)


Role Assignment: Operator1 has been successfully assigned the Microsoft Sentinel Contributor role at the RG2 scope.

![image_alt](https://github.com/PhenyoMB/sc-500-labs/blob/55d63ea5d0309dd13cc9b488eb859339de33f4eb/01-Sentinel-Environment/Assign%20a%20MS%20Sentinel%20Role%20To%20A%20User%202.png)


Data Retention: The workspace is configured to retain data for 180 days.

![image_alt](https://github.com/PhenyoMB/sc-500-labs/blob/55d63ea5d0309dd13cc9b488eb859339de33f4eb/01-Sentinel-Environment/Configure%20Data%20Retention.png)
