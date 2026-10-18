# Secure Azure with Microsoft Defender for Cloud Compliance Controls

## Lab Overview

**Objective:** Practise configuring Azure infrastructure and security controls that support network segmentation, monitoring, controlled administrative access, secret protection, and private connectivity.

This hands-on lab is documented through screenshots grouped into seven stages. The folder and image names indicate the tasks performed; where a screenshot's contents could not be independently inspected, details are described at the task level rather than as verified configuration values.

**Microsoft services and technologies represented in the lab:**

- Microsoft Azure resource groups and virtual networks
- Network Security Groups (NSGs) and Application Security Groups (ASGs)
- Azure Virtual Machines
- Log Analytics workspaces
- Azure Monitor Agent and Data Collection Rules (DCRs)
- Just-in-time (JIT) VM access
- Azure Key Vault
- Azure SQL logical server and private endpoint

**Environment and prerequisites**

The evidence is organised around Azure Portal workflows. Performing these tasks generally requires an Azure subscription, permission to create and configure the relevant resources, and appropriate access to security settings. Exact subscription details, resource names, regions, SKUs, and role assignments are not documented here because they could not be verified from the available file listing.

> **Portfolio note:** This README documents a hands-on learning lab, not a production deployment or an independent security audit.

## Concepts Learned

### Resource groups and virtual networks

A resource group provides a management boundary for related Azure resources. A virtual network (VNet) provides private network connectivity for Azure resources. Organising resources into subnets and applying network controls helps define where traffic is allowed.

### Network Security Groups and Application Security Groups

An NSG applies inbound and outbound traffic rules to supported network interfaces or subnets. An ASG groups virtual machine network interfaces according to application roles, allowing NSG rules to refer to logical groups instead of maintaining separate rules for every interface.

The screenshots' filenames indicate that NSGs, security rules, ASGs, and associations between VM network interfaces and ASGs are included in the lab.

### Log Analytics, Azure Monitor Agent, and Data Collection Rules

A Log Analytics workspace is a destination for supported log and telemetry data. The Azure Monitor Agent collects supported monitoring data from machines, while a DCR specifies what data to collect and where to send it.

Correct configuration of these components is important for centralised monitoring and for making relevant telemetry available to downstream monitoring or security workflows. The available filenames document setup activities, but do not by themselves prove that logs arrived or were queried successfully.

### Just-in-time VM access

JIT access reduces the period during which selected VM management ports are exposed. Instead of leaving management access broadly open, an authorised user requests access for a limited period according to the configured policy.

Enabling a JIT setting and successfully requesting access are separate outcomes. This lab's screenshot filenames indicate both an enablement workflow and a VM access request workflow.

### Azure Key Vault and soft delete

Azure Key Vault is used to manage secrets, keys, and certificates. Network access controls can help restrict which network paths can reach a vault. Soft delete helps recover supported vault objects after accidental deletion during the configured retention period.

Creating a vault, configuring its network restrictions, and checking soft-delete settings are distinct tasks. The presence of screenshots for these tasks is not, on its own, proof that every restriction was tested from an allowed and a denied network.

### Azure SQL private endpoints

A private endpoint uses a private IP address in a virtual network to reach a supported Azure service through Azure Private Link. This can reduce reliance on public network exposure, provided name resolution, routing, service settings, and access controls are configured correctly.

The final screenshot group is named around an Azure SQL server, a private endpoint, and connectivity tests. The exact test results should be confirmed from the screenshots before claiming that connectivity succeeded or that public access was fully restricted.

## Implementation

### 1. Create the resource group and virtual network

The first stage documents the creation of an Azure resource group and virtual network, followed by network security controls and virtual machines.

The screenshot filenames indicate these activities:

- Create a resource group and virtual network.
- Create an NSG and define security rules.
- Associate an NSG with a subnet.
- Create ASGs for workloads with similar functions.
- Associate VM network interfaces with the relevant ASGs.
- Create two VMs in the virtual network.

These controls are intended to establish the network foundation and demonstrate how traffic rules can be organised around network location and workload role.

![Creating a resource group and virtual network](./01-Create%20an%20azure%20resource%20group%20and%20virtual%20network/Create%20a%20resource%20group%20and%20virtual%20network%201.png)

![Additional resource group and virtual network configuration](./01-Create%20an%20azure%20resource%20group%20and%20virtual%20network/Create%20a%20resource%20group%20and%20virtual%20network%202.png)

![Alternative resource group and virtual network workflow screenshot](./01-Create%20an%20azure%20resource%20group%20and%20virtual%20network/Create%20an%20AZ%20Resource%20Group%20and%20VN%20Network.png)

![Additional Azure resource group and virtual network screenshot](./01-Create%20an%20azure%20resource%20group%20and%20virtual%20network/Create%20an%20AZ%20Resource%20Group%20and%20VN%20Network%202.png)

![Creating a network security group](./01-Create%20an%20azure%20resource%20group%20and%20virtual%20network/Create%20a%20network%20security%20group%20to%20secure%20network%20traffic%20in%20your%20virtual%20network.png)

![Defining NSG security rules for the virtual network subnet](./01-Create%20an%20azure%20resource%20group%20and%20virtual%20network/Create%20security%20rules%20for%20the%20network%20security%20group%20with%20the%20subnet%20of%20the%20virtual%20network%20created%20earlier.png)

![Associating an NSG with a subnet](./01-Create%20an%20azure%20resource%20group%20and%20virtual%20network/Associate%20network%20security%20group%20to%20subnet.png)

![Creating Application Security Groups](./01-Create%20an%20azure%20resource%20group%20and%20virtual%20network/Create%20application%20security%20groups%20to%20enable%20you%20to%20group%20together%20servers%20with%20similar%20functions%2C%20such%20as%20web%20servers.png)

![Associating the first VM network interface with an Application Security Group](./01-Create%20an%20azure%20resource%20group%20and%20virtual%20network/Associate%20network%20interfaces%20to%20an%20application%20security%20group%20vm1%20asg-mgmt.png)

![Associating the second VM network interface with an Application Security Group](./01-Create%20an%20azure%20resource%20group%20and%20virtual%20network/Associate%20network%20interfaces%20to%20an%20application%20security%20group%20vm2%20asg-web.png)

![Creating the virtual machines](./01-Create%20an%20azure%20resource%20group%20and%20virtual%20network/Create%20two%20virtual%20machines%20%28VMs%29%20in%20the%20virtual%20network%20you%20created%20earlier%20vms.png)

![Creating the first virtual machine](./01-Create%20an%20azure%20resource%20group%20and%20virtual%20network/Create%20two%20virtual%20machines%20%28VMs%29%20in%20the%20virtual%20network%20you%20created%20earlier%20vm1.png)

![Creating the second virtual machine](./01-Create%20an%20azure%20resource%20group%20and%20virtual%20network/Create%20two%20virtual%20machines%20%28VMs%29%20in%20the%20virtual%20network%20you%20created%20earlier%20vm2.png)

### 2. Create a Log Analytics workspace

The second stage is dedicated to creating a Log Analytics workspace. A workspace provides a central destination for supported Azure Monitor log data and can be used by monitoring and security solutions.

The available evidence identifies the workspace creation task, but the workspace name, region, retention configuration, and successful ingestion of data have not been independently verified.

![Creating a Log Analytics workspace](./02-Use%20the%20Log%20Analytics%20workspaces%20menu%20to%20create%20a%20workspace/Use%20the%20Log%20Analytics%20workspaces%20menu%20to%20create%20a%20workspace.png)

### 3. Configure a Data Collection Rule and Azure Monitor Agent

The third stage documents work with a Data Collection Rule and the Azure Monitor Agent. These components work together to collect supported monitoring data from a machine and route it to an appropriate destination.

When reviewing this configuration, the important details to verify are the targeted resources, data sources, selected data, destination workspace, and agent installation or provisioning status.

![Data Collection Rule and Azure Monitor Agent setup, step 1](./03-Create%20and%20define%20a%20Data%20Collection%20Rule%2C%20and%20install%20the%20Azure%20Monitor%20Agent/Create%20and%20define%20a%20Data%20Collection%20Rule%2C%20and%20install%20the%20Azure%20Monitor%20Agent%201.png)

![Data Collection Rule and Azure Monitor Agent setup, step 2](./03-Create%20and%20define%20a%20Data%20Collection%20Rule%2C%20and%20install%20the%20Azure%20Monitor%20Agent/Create%20and%20define%20a%20Data%20Collection%20Rule%2C%20and%20install%20the%20Azure%20Monitor%20Agent%202.png)

![Data Collection Rule and Azure Monitor Agent setup, step 3](./03-Create%20and%20define%20a%20Data%20Collection%20Rule%2C%20and%20install%20the%20Azure%20Monitor%20Agent/Create%20and%20define%20a%20Data%20Collection%20Rule%2C%20and%20install%20the%20Azure%20Monitor%20Agent%203.png)

### 4. Enable just-in-time access for virtual machines

The fourth stage documents enabling JIT access for VMs and requesting access through the VM connection workflow.

JIT is intended to reduce unnecessary exposure of management ports. To validate the control fully, check the configured ports, permitted source ranges, maximum request duration, and the result of an access request. Those exact settings and outcomes are not asserted here without visual confirmation.

![Enabling JIT access for virtual machines, step 1](./04-Enable%20JIT%20on%20your%20VMs%20from%20Azure%20virtual%20machines/Enable%20JIT%20on%20your%20VMs%20from%20Azure%20virtual%20machines%201.png)

![Enabling JIT access for virtual machines, step 2](./04-Enable%20JIT%20on%20your%20VMs%20from%20Azure%20virtual%20machines/Enable%20JIT%20on%20your%20VMs%20from%20Azure%20virtual%20machines%202.png)

![Enabling JIT access for virtual machines, step 3](./04-Enable%20JIT%20on%20your%20VMs%20from%20Azure%20virtual%20machines/Enable%20JIT%20on%20your%20VMs%20from%20Azure%20virtual%20machines%203.png)

![Requesting access to a JIT-enabled VM](./04-Enable%20JIT%20on%20your%20VMs%20from%20Azure%20virtual%20machines/Request%20access%20to%20a%20JIT-enabled%20VM%20from%20the%20Azure%20virtual%20machine%27s%20connect%20page.png)

### 5. Create Azure Key Vault and configure network settings

The fifth stage documents creating an Azure Key Vault and configuring its firewall and virtual network settings.

Key Vault is used to manage sensitive application material such as secrets, keys, and certificates. Network restrictions can limit the paths through which the vault is reachable, but should be designed alongside identity-based permissions and the application's required access paths.

The filenames indicate that vault creation and network settings were documented. The exact firewall configuration and whether access was tested from allowed and blocked paths remain unverified.

![Creating an Azure Key Vault, step 1](./05-Use%20the%20Azure%20portal%20to%20create%20an%20Azure%20Key%20Vault/Use%20the%20Azure%20portal%20to%20create%20an%20Azure%20Key%20Vault%201.png)

![Creating an Azure Key Vault, step 2](./05-Use%20the%20Azure%20portal%20to%20create%20an%20Azure%20Key%20Vault/Use%20the%20Azure%20portal%20to%20create%20an%20Azure%20Key%20Vault%202.png)

![Configuring Key Vault firewall and virtual network settings, step 1](./05-Use%20the%20Azure%20portal%20to%20create%20an%20Azure%20Key%20Vault/Configure%20Key%20Vault%20firewall%20and%20virtual%20network%20settings%201.png)

![Configuring Key Vault firewall and virtual network settings, step 2](./05-Use%20the%20Azure%20portal%20to%20create%20an%20Azure%20Key%20Vault/Configure%20Key%20Vault%20firewall%20and%20virtual%20network%20settings%202.png)

### 6. Verify Key Vault soft delete

The sixth stage is named around checking whether soft delete is enabled on a Key Vault and enabling it. Soft delete provides a recovery mechanism for supported deleted vault objects during the configured retention period.

For a complete validation, review the vault's soft-delete status and applicable retention settings. The screenshot filename establishes the purpose of this stage, but the actual setting and retention value have not been independently confirmed.

![Checking and enabling Key Vault soft delete](./06-Verify%20if%20soft%20delete%20is%20enabled%20on%20a%20key%20vault%20and%20enable%20soft%20delete/Verify%20if%20soft%20delete%20is%20enabled%20on%20a%20key%20vault%20and%20enable%20soft%20delete.png)

### 7. Configure Azure SQL private connectivity

The final stage documents a second resource group and virtual network workflow, virtual machine creation, an Azure SQL logical server, a private endpoint, and a public IP access-rule task.

A private endpoint provides a private network interface for reaching a supported Azure service over Private Link. A complete validation should confirm the endpoint connection state, private DNS resolution from the intended network, and connectivity from an appropriate client. Public firewall rules and private endpoint access should also be reviewed together to understand which access paths remain available.

The screenshots are named for connectivity tests, but their contents and results have not been visually verified. Therefore, this README does not claim that the tests succeeded or that public connectivity was disabled.

![Creating a virtual machine, step 1](./07-Create%20a%20resource%20group%20and%20virtual%20network/Create%20a%20virtual%20machine%201.png)

![Creating a virtual machine, step 2](./07-Create%20a%20resource%20group%20and%20virtual%20network/Create%20a%20virtual%20machine%202.png)

![Creating a virtual machine, step 3](./07-Create%20a%20resource%20group%20and%20virtual%20network/Create%20a%20virtual%20machine%203.png)

![Creating an Azure SQL server and private endpoint](./07-Create%20a%20resource%20group%20and%20virtual%20network/Create%20an%20Azure%20SQL%20server%20and%20private%20endpoint.png)

![Configuring public IP access rules for the Azure SQL logical server](./07-Create%20a%20resource%20group%20and%20virtual%20network/Allow%20certain%20public%20internet%20IP%20addresses%20to%20access%20your%20Azure%20SQL%20logical%20server.png)

![Testing private endpoint connectivity, step 1](./07-Create%20a%20resource%20group%20and%20virtual%20network/Test%20connectivity%20to%20private%20endpoint%201.png)

![Testing private endpoint connectivity, step 2](./07-Create%20a%20resource%20group%20and%20virtual%20network/Test%20connectivity%20to%20private%20endpoint%202.png)

![Testing private endpoint connectivity, step 3](./07-Create%20a%20resource%20group%20and%20virtual%20network/Test%20connectivity%20to%20private%20endpoint%203.png)

## Validation and Results

The repository contains screenshots whose filenames correspond to these configuration activities:

- Creation of a resource group, virtual network, NSG, ASGs, and VMs.
- Creation of a Log Analytics workspace.
- Configuration of a DCR and Azure Monitor Agent.
- JIT access enablement and a VM access request workflow.
- Azure Key Vault creation and firewall/network settings.
- Key Vault soft-delete review.
- Azure SQL logical server and private endpoint configuration, including named connectivity-test screenshots.

These are evidence of the lab's documented workflow, not independent confirmation of every final state. Before treating the lab as fully validated, review the screenshots for visible success indicators and, where possible, record test results for data ingestion, JIT access, Key Vault network restrictions, soft-delete configuration, private DNS resolution, and private endpoint connectivity.

## Key Takeaways

- Network security involves combining subnet-level controls, NSG rules, and workload grouping with ASGs.
- Monitoring requires more than creating a workspace: collection rules, agents, data sources, destinations, and actual ingestion all matter.
- JIT access is intended to minimise standing exposure of VM management ports.
- Key Vault security includes both identity permissions and network access controls.
- Soft delete is a recovery control and should be reviewed alongside retention and recovery requirements.
- Private endpoints can provide private connectivity to supported Azure services, but DNS and service access settings are essential to making the intended path work.
- Security configuration should be validated with observable results rather than inferred from the presence of a settings page.
