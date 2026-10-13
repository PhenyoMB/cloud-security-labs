**Simulated Attacks**

**Lab Overview**

Objective: Perform a simulated privilege escalation attack to validate that the NRT analytics rule detects the activity, creates an incident, and the automation rule assigns ownership to Operator1.

Microsoft Services Used: Microsoft Sentinel, Azure Virtual Machines, Azure Run Command.

Environment and Prerequisites: Azure subscription, Resource Group RG2, vm1 virtual machine (running), and the lab1-ws workspace with the NRT rule and automation rule configured (from Lab 03).

**Concepts Learned**

Simulated Attacks: A safe method to test detection logic by executing known adversarial techniques (in this case, adding a user to the local administrators group) in a controlled environment.

Event ID 4732: The Windows Security Event ID generated when a member is added to a security-enabled local group. This is a common indicator of privilege escalation.

NRT Rule Validation: Confirming that Near-Real-Time rules trigger quickly (within minutes) after the malicious activity occurs.

Automation Rule Execution: Validating that incident ownership is automatically assigned without manual intervention.

Incident Investigation Basics: Exploring the incident details pane to review owner, tactics, severity, and available evidence.

**Implementation**

Simulated a Privilege Escalation Attack:

Navigated to vm1 in the Azure portal and opened the Run command pane.

Executed a PowerShell script to create three separate local admin accounts (testuser1, testuser2, testuser3), each using the commands:

net user <username> /add

net user <username> ThePassword1!

net localgroup administrators <username> /add

Validated Incident Generation:

Navigated to Microsoft Sentinel > Threat management > Incidents.

Observed that the NRT rule generated a new incident for each user creation event.

Opened the incident details pane to verify the Owner and Tactics fields.

**Validation and Results**

Attack Execution: The Run command output confirmed "The command completed successfully" three times for each of the three user accounts, verifying the simulated attack worked as intended.

![image_alt](https://github.com/PhenyoMB/sc-500-labs/blob/c1ee9d1eb5fbdfc052cacd43f9f90597541acf93/04/Perform%20a%20Simulated%20Privilege%20Escalation%20Attack.png)
![image_alt](https://github.com/PhenyoMB/sc-500-labs/blob/c1ee9d1eb5fbdfc052cacd43f9f90597541acf93/04/Perform%20a%20Simulated%20Privilege%20Escalation%20Attack%202.png)
![image_alt](https://github.com/PhenyoMB/sc-500-labs/blob/c1ee9d1eb5fbdfc052cacd43f9f90597541acf93/04/Perform%20a%20Simulated%20Privilege%20Escalation%20Attack%203.png)

Incident Creation: Three separate incidents were generated, all titled lab-nrt-query with Medium severity.

Incident Ownership: The automation rule successfully assigned all three incidents to Operator1-66127721.

Tactic Mapping: The incidents were correctly tagged with the Privilege Escalation tactic based on the NRT rule's configuration.

Incident Timeline: The incidents were created within the same hour as the simulated attack, demonstrating the low-latency detection of NRT rules.

![image_alt](https://github.com/PhenyoMB/sc-500-labs/blob/c1ee9d1eb5fbdfc052cacd43f9f90597541acf93/04/Verify%20an%20Incident%20Is%20Created%20From%20The%20Simulated%20Attack%202.png)
![image_alt](https://github.com/PhenyoMB/sc-500-labs/blob/c1ee9d1eb5fbdfc052cacd43f9f90597541acf93/04/Verify%20an%20Incident%20Is%20Created%20From%20The%20Simulated%20Attack.png)

