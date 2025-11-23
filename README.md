# Sentinel-Lab-Mitre-Attack
## Threat Detection with Microsoft Sentinel (MITRE T1059.001)
### Objective To build a cloud-based Security Operations Center (SOC) environment, ingest logs from an on-premises endpoint, and simulate/detect an obfuscated PowerShell attack (MITRE ATT&CK T1059.001) often used by malware to evade defense mechanisms.

Tools Used

SIEM: Microsoft Sentinel (Azure)

Endpoint: Windows 11 Enterprise (Virtual Machine)

Log Collection: Azure Monitor Agent (AMA) & Azure Arc

Query Language: KQL (Kusto Query Language)

Step 1: Environment Setup & Hardening I configured a Windows 11 VM and connected it to Azure using Azure Arc. To ensure visibility into the attack, I enabled "Process Creation" auditing and command-line logging via the Windows Registry/Group Policy.



Caption: Enabling Command Line Auditing to capture full argument strings.
