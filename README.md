# Sentinel-Lab-Mitre-Attack
## Threat Detection with Microsoft Sentinel (MITRE T1059.001)
### Objective To build a cloud-based Security Operations Center (SOC) environment, ingest logs from an on-premises endpoint, and simulate/detect an obfuscated PowerShell attack (MITRE ATT&CK T1059.001) often used by malware to evade defense mechanisms.

Tools Used

SIEM: Microsoft Sentinel (Azure)

Endpoint: Windows 11 Enterprise (Virtual Machine)

Log Collection: Azure Monitor Agent (AMA) & Azure Arc

Query Language: KQL (Kusto Query Language)

Step 1: Environment Setup & Hardening I configured a Windows 11 VM and connected it to Azure using Azure Arc. To ensure visibility into the attack, I enabled "Process Creation" auditing and command-line logging via the Windows Registry/Group Policy.

https://github.com/jammerthewelsh/Sentinel-Lab-Mitre-Attack/blob/main/AD%20group%20policy.png

Caption: Enabling Command Line Auditing to capture full argument strings.

Step 2: The Attack (Simulation) I simulated an adversary using Base64 encoding to obfuscate a PowerShell command. This technique allows attackers to hide their actual intent (e.g., downloading malware) from basic text-based filters.

(https://github.com/jammerthewelsh/Sentinel-Lab-Mitre-Attack/blob/main/powershell%20simulated%20attack.png)

Caption: Executing the obfuscated payload: powershell.exe -EncodedCommand...

Step 3: Detection (The Hunt) Using Microsoft Sentinel, I wrote a KQL query to hunt for the specific execution pattern. I filtered for Event ID 4688 (Process Creation) and searched for the "-EncodedCommand" parameter, which is a high-fidelity indicator of this technique.

[Insert your final Sentinel Log Result Screenshot here]

