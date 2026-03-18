<h1>Project 3: Brute Force Attack & Detection</h1>

<h2>Overview</h2>
This project simulates a real-world brute force attack against a Windows 11 machine and demonstrates how to detect and analyze the activity using Microsoft Sentinel and Defender.

<h3>Lab Architecture</h3>

  - Host Machine: macOS (VMware Fusion)
  - Attacker: Kali Linux VM
  - Target: Windows 11 VM
  - SIEM: Azure Sentinel
  - EDR: Microsoft Defender for Endpoint
  - Log Source: Windows Security Events (Event ID 4625)

<h3>Objective</h3>

  1. Modify Windows 11 Audit Policy to enable logon events (success and failure)
  2. Expose RDP services on the Windows host
  3. Perform reconnaissance using Nmap
  4. Execute a brute force attack using Hydra
  5. Ingest logs into Sentinel
  6. Detect the attack using KQL queries
  7. Generate alerts and analyze incidents

<h2>Step 1: Modifying Windows Audit Policy</h2>

Before performing any attack simulations, I enabled auditing on the Windows 11 target to ensure failed logon events would be captured and forwarded to Microsoft Sentinel.

**Audit Policy Enabled:**
- Audit Logon Events → Failure
- Audit Logon Events → Success

<h2>Step 2: Reconissance using Nmap</h2>

I used Nmap to identify open ports on the Windows 11 target.

<IMAGE>

Key Findings:
- Port 3389 (RDP) open
- Port 445 (SMB) open
- Port 5357 (WS-Discovery) open

This confirms that RDP is exposed and can be targeted for brute force attacks.

<h2>Step 3: Brute Force Attack</h2>

I used Hydra to perform a password brute force attack against the RDP service.

<Image>

**Behavior Observed:**
- Multiple failed login attempts
- Rapid authentication requests
- No successful login achieved

This activity generates Windows Security Event ID 4625 (failed logons).

<h2>Step 4: Microsoft Sentinel Log Analysis</h2>

The attack logs were ingested into Microsoft Sentinel.

<IMAGE>

Key Insights:
- Source IP: 192.168.180.128 (Kali attacker)
- Target Account: james
- Failed attempts detected in 5-minute intervals

<h2>Step 5: Alert Creation</h2>

I created a Scheduled Query Rule in Sentinel to detect brute force behavior.

**Rule:**
- Trigger when failed logons > 5
- Based on Event ID 4625
- Grouped by IP address and account

Alert Details:
- Severity: Medium
- Category: Credential Access
- Detection Source: Scheduled Query

<h2>Step 6: Microsoft Defender Incidents & Alerts</h2>

Multiple alerts were generated for failed logon attempts (brute force)

<IMAGE>

Findings:
- Repeated failed login attempts from a single IP
- Pattern consistent with brute force attack
- No successful authentication observed

SOC Actions:
- Identified source IP
- Confirmed attack pattern
- Recommendedations include blocking IP or enforcing account lockout policies

<h2>Key Takeaways</h2>

- Brute force attacks generate identifiable patterns in Event ID 4625 logs
- KQL can be used to detect abnormal authentication behavior
- Microsoft Sentinel enables real-time alerting and investigation
- Detection engineering is critical for proactive security monitoring
