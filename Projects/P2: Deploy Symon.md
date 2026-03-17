<h1>Project 2: Deploy Symon</h1>

<h2>Overview</h2>

This project demonstrates the deployment and integration of Sysmon (System Monitor) with Microsoft Sentinel for endpoint telemetry collection and security monitoring. Sysmon extends the default Windows logging capabilities by generating high-fidelity security events, including:

- Process creation
- Network connections
- File creation
- Registry modifications
- Driver loads
- Process termination

These events are collected from a Windows virtual machine, forwarded to Azure Log Analytics, and analyzed in Microsoft Sentinel using Kusto Query Language (KQL).

The objective of this deployment is to simulate a real-world SOC logging pipeline, where endpoint telemetry is ingested into a SIEM platform for detection, investigation, and threat hunting.

<h2>Step 1: Installing and Running Sysmon</h2>

Sysmon was installed on the Windows VM and configured to run as a system service.

<p align="left">
<img src="https://i.imgur.com/i5NAGi8.png" height="50%" width="50%"/>

<h2>Step 2: Verifying Sysmon Event Logs in Windows</h2>

After installation, Sysmon events appear in Windows Event Viewer.

<b>Logs Location:</b>

- Microsoft → Windows → Windows → Sysmon → Operational

<b>Example events observed:</b>

- Event ID 1 – Process creation

- Event ID 5 – Process termination

- Event ID 16 – Sysmon configuration change

<p align="left">
<img src="https://i.imgur.com/6y2Ze2x.png" height="75%" width="75%"/>

These events confirm that Sysmon is actively monitoring and logging system activity.

<h2>Step 3: Configuring Sentinel Data Collection</h2>

To ingest Sysmon telemetry into Sentinel, a Data Collection Rule (DCR) was created.

<b>Configuration:</b>

Data Source Type: Windows Event Logs
Log Source:
Microsoft-Windows-Sysmon/Operational

<p align="left">
<img src="https://i.imgur.com/iBDfQGQ.png" height="75%" width="75%"/>

This ensures that Sysmon logs are forwarded from the endpoint to Azure Log Analytics.

<h2>Step 4: Verifying Sysmon Logs in Microsoft Sentinel</h2>

Once ingestion was configured, logs were queried within Microsoft Sentinel using KQL.

<b>Query used:</b>

Event
| where Source == "Microsoft-Windows-Sysmon"
| sort by TimeGenerated desc

<p align="left">
<img src="https://i.imgur.com/brtVS66.png" height="75%" width="75%"/>

This confirms that Sysmon telemetry is successfully flowing into the SIEM.

<h2>Data Flow Explanation</h2>

<b>The log pipeline works as follows:</b>

  1. Sysmon monitors system activity
  2. Events are written to Windows Event Logs
  3. Azure Monitor Agent collects the logs
  4. Logs are forwarded via a Data Collection Rule
  5. Logs are stored in Log Analytics Workspace
  6. Microsoft Sentinel queries and analyzes the data

**This architecture allows security teams to perform:**

- Threat detection
- Log correlation
- Incident investigation
- Threat hunting using KQL
- Security Value of Sysmon

Sysmon provides telemetry that is extremely valuable for security detection.

**Examples include:**

- Event ID	Detection Use
1	Suspicious process execution
3	Network connections
7	DLL injection
11	File creation
13	Registry modification

By ingesting these logs into Sentinel, analysts can build detection rules and alerts for malicious activity.

<h2>Key Skills Demonstrated</h2>

- Windows endpoint logging
- Sysmon deployment and verification
- Azure Monitor Agent configuration
- Microsoft Sentinel data ingestion
- KQL querying for security telemetry
- SOC-style log pipeline architecture
