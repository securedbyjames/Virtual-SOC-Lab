<h1>Azure Sentinel SOC Lab Setup</h1>

<h2>Overview</h2>

This setup demonstrates a SOC monitoring pipeline using Microsoft Sentinel to collect and analyze Windows security logs from a monitored endpoint.

The lab simulates a real-world SIEM deployment by forwarding Windows event logs from a VM to Azure Sentinel using Azure Monitor Agent and Data Collection Rules.

<h2>Setup</h2>

  1. Navigate to Azure Arc in the Azure Portal
  2. Select "Add a single server"
  3. Generate the onboarding script
  4. Run the script in PowerShell on the Windows VM
  5. Verify the machine appears in Azure Arc

<h2>Lab Architecutre</h2>
<p align="left">
<img src="https://i.imgur.com/iIYZFLT.png" height="80%" width="80%"/>

<h3>Azure Arc Machine</h3>

Azure Arc allows on-premises or non-Azure machines to be managed through Azure as hybrid resources. This view confirms that the Windows VM has successfully registered with Azure Arc and is connected to the Azure environment, enabling centralized management and monitoring.
<br>
<p align="left">
<img src="https://i.imgur.com/SOZPSur.png" height="80%" width="80%"/>

<h3>Azure Monitor Agent Extension</h3>
The Azure Monitor Agent (AMA) extension is installed on the machine to collect telemetry and system logs. It enables the VM to send monitoring data, including Windows Event Logs, to Azure services such as Log Analytics and Microsoft Sentinel for analysis and security monitoring.

<br><p align="left">
<img src="https://i.imgur.com/N3cu7kV.png" height="80%" width="80%"/>

<h3>Data Collection Rule</h3>
A Data Collection Rule (DCR) defines which logs and telemetry should be collected from monitored machines and where that data should be sent. In this lab, the DCR specifies that Windows event logs from the VM are forwarded to the Log Analytics workspace used by Microsoft Sentinel.

<br><p align="left">
<img src="https://i.imgur.com/0vKtDVN.png" height="80%" width="80%"/>

<h3>Log Analytics Workspace</h3>
The Log Analytics Workspace acts as the central data repository for collected logs. Telemetry gathered by the Azure Monitor Agent is stored here and can be queried using Kusto Query Language (KQL) for monitoring, analysis, and threat detection.

<!-- <p align="left">
<img src="https://i.imgur.com/iIYZFLT.png" height="80%" width="80%"/> -->

<h3>Sentinel Workspace</h3>
Microsoft Sentinel is Azure’s cloud-native SIEM and security analytics platform. It uses data stored in the Log Analytics workspace to detect threats, investigate security events, and provide centralized visibility into system activity across monitored resources.

<!-- <p align="left">
<img src="https://i.imgur.com/iIYZFLT.png" height="80%" width="80%"/> -->

<h2>Query Examples</h2>
