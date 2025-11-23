# Sentinel-Lab-Mitre-Attack
## Threat Detection with Microsoft Sentinel (MITRE T1059.001)
### Objective To build a cloud-based Security Operations Center (SOC) environment, ingest logs from an on-premises endpoint, and simulate/detect an obfuscated PowerShell attack (MITRE ATT&CK T1059.001) often used by malware to evade defense mechanisms.

Tools Used

SIEM: Microsoft Sentinel (Azure)

Endpoint: Windows 11 Enterprise (Virtual Machine)

Log Collection: Azure Monitor Agent (AMA) & Azure Arc

Query Language: KQL (Kusto Query Language)

Step 1: Environment Setup & Hardening I configured a Windows 11 VM and connected it to Azure using Azure Arc. To ensure visibility into the attack, I enabled "Process Creation" auditing and command-line logging via the Windows Registry/Group Policy.

<img src="https://github.com/jammerthewelsh/Sentinel-Lab-Mitre-Attack/blob/main/AD%20group%20policy.png" width="800" alt="Detection Evidence">


Step 2: The Attack (Simulation) I simulated an adversary using Base64 encoding to obfuscate a PowerShell command. This technique allows attackers to hide their actual intent (e.g., downloading malware) from basic text-based filters.

<img src="https://github.com/jammerthewelsh/Sentinel-Lab-Mitre-Attack/blob/main/powershell%20simulated%20attack.png" width="800" alt="Detection Evidence">


Step 3: Detection (The Hunt) Using Microsoft Sentinel, I wrote a KQL query to hunt for the specific execution pattern. I filtered for Event ID 4688 (Process Creation) and searched for the "-EncodedCommand" parameter, which is a high-fidelity indicator of this technique.

<img src="https://github.com/jammerthewelsh/Sentinel-Lab-Mitre-Attack/blob/main/KQL%20hunt%20output.png" width="800" alt="Detection Evidence">

Lessons Learned 

Log Latency: I learned that Azure Arc agents cache logs locally if the connection drops (e.g., due to time drift), ensuring data integrity once the connection is restored.

The Importance of Field Mapping: The detection was only possible because I explicitly configured the Data Collection Rule (DCR) to forward "Security Events," proving that a SIEM is only as good as its data sources.
