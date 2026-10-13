**Configure Microsoft Sentinel Data Collection Rules**

**Lab Overview**

Objective: Configure a Data Collection Rule (DCR) for Windows Security Events via AMA, create a Near-Real-Time (NRT) analytics rule, and configure an automation rule to assign incident ownership.

Microsoft Services Used: Microsoft Sentinel, Azure Monitor Agent (AMA), Log Analytics Workspace, Azure RBAC.

Environment and Prerequisites: Azure subscription, Resource Group RG2, vm1 virtual machine, and the lab1-ws Log Analytics workspace with Microsoft Sentinel enabled (from Lab 01).

**Concepts Learned**

Data Collection Rules (DCRs): The modern method for defining what data to collect, how to process it, and where to send it. DCRs provide granular control, allowing you to scope data collection to specific resources (like vm1) rather than entire subscriptions.

Azure Monitor Agent (AMA): Replaces the legacy Log Analytics agent. It uses DCRs to collect Windows Security Events and forward them to Sentinel.

Near-Real-Time (NRT) Rules: Analytics rules that run approximately every minute to detect threats with minimal latency. They are designed for high-priority detections where immediate response is critical.

Automation Rules: Allow for centralized incident management. They can assign ownership, change severity, or add tags to incidents. They are different from Playbooks (which execute complex logic).

Incident Ownership vs. Azure RBAC Owner: The "Assign owner" action in Sentinel sets the incident owner within the SIEM platform. It does not grant the user the Azure RBAC "Owner" role on the underlying resources.

**Implementation**

Configured a Data Collection Rule (DCR):

Navigated to the Windows Security Events via AMA connector.

Created a new DCR named lab1-dcr in Resource Group RG2.

Scoped the DCR specifically to the vm1 virtual machine.

Selected All Events (or "All Security Events") for collection.

Created an NRT Analytics Rule:

Created a new NRT query rule named lab-nrt-query.

Assigned the MITRE ATT&CK tactic Privilege Escalation.

Entered the KQL query: SecurityEvent | where EventID == 4732 | where TargetAccount == "Builtin\\Administrators".

Enabled incident creation for the rule.

Configured an Automation Rule:

Created a new automation rule named lab-automation-rule.

Set the trigger to When incident is created.

Configured an action to Assign owner to Operator1-66127721.

**Validation and Results**

DCR Created: The DCR lab1-dcr was successfully created and validation passed. It is scoped exclusively to vm1.

![image_alt](https://github.com/PhenyoMB/sc-500-labs/blob/6e21c20c557dc17ec8645ead26eea5109f081181/03-/Configure%20Data%20Collection%20rules%20(DCRs)%20in%20Sentinel.png)
![image_alt](https://github.com/PhenyoMB/sc-500-labs/blob/6e21c20c557dc17ec8645ead26eea5109f081181/03-/Configure%20Data%20Collection%20rules%20(DCRs)%20in%20Sentinel%20%202.png)

NRT Rule Enabled: The lab-nrt-query rule was created successfully. It is enabled, uses the required KQL query, and maps to the Privilege Escalation tactic.

![image_alt](https://github.com/PhenyoMB/sc-500-labs/blob/6e21c20c557dc17ec8645ead26eea5109f081181/03-/Create%20a%20Near%20Real-Time%20(NRT)%20Query%20Detection.png)

Analytics Rules List: The Sentinel Analytics page confirms 3 active rules, including the newly created lab-nrt-query (NRT type), alongside the scheduled rule from Lab 02 and the default Fusion rule.

![image_alt](https://github.com/PhenyoMB/sc-500-labs/blob/6e21c20c557dc17ec8645ead26eea5109f081181/03-/Create%20a%20Near%20Real-Time%20(NRT)%20Query%20Detection%202.png)

Automation Rule Enabled: The lab-automation-rule was created and is enabled.

![image_alt](https://github.com/PhenyoMB/sc-500-labs/blob/6e21c20c557dc17ec8645ead26eea5109f081181/03-/Configure%20Automation%20in%20Microsoft%20Sentinel.png)
![image_alt](https://github.com/PhenyoMB/sc-500-labs/blob/6e21c20c557dc17ec8645ead26eea5109f081181/03-/Configure%20Automation%20in%20Microsoft%20Sentinel%202.png)


