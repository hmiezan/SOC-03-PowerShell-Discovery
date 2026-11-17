### Overview
Following initial access and SMB share discovery identified in previous investigations Lab 01 and lab 02 , the attacker launched PowerShell and began collecting information about the compromised host.

### Lab Environment
- Windows 11 10.161.200.x  ( compromised host)
- Security Onion SIEM
- Elastic Agent Installed

### Attack Execution

The following commands were executed:

- whoami
- hostname
- ipconfig /all
- net user
- net localgroup administrators
- systeminfo

### Detection and Investigation findings
Detection Query: process.name:powershell.exe 
PowerShell execution was successfully identified within Security Onion.

### Evidence Collected: Username / Hostname / Process Information / Timestamp

PowerShell Execution
<img width="1023" height="72" alt="image" src="https://github.com/user-attachments/assets/e14aaf59-54fe-4a0b-9661-ef6b3bfac97d" />



Child Process Analysis
<img width="1241" height="734" alt="image" src="https://github.com/user-attachments/assets/e33e03a8-197c-4000-9da5-1eef57de4b08" />


#### MITRE ATT&CK Mapping
- Tactic (Execution	)- PowerShell :	T1059.001 
- Tactic (Discovery) - Technique (System Owner/User Discovery): T1033
- Tactic (Discovery) - Technique (System Information Discovery): T1082
- Tactic (Discovery) - Technique (Account Discovery): T1087
- Tactic (Discovery) - Technique (Permission Group Discovery): T1069

#### Investigation timeline

- 20:21	PowerShell launched
- 20:21.26	whoami executed
- 20:21.34	net user executed
- 20:21.51	net localgroup administrators executed
- 20:22.21	systeminfo executed
- 20:23.31	ipconfig /all executed
- 20:27	SOC investigation initiated


#### Analysis
The attacker executed PowerShell and performed several host discovery commands designed to gather information about:

- Current user context
- Operating system details
- Network configuration
- Local users
- Administrative accounts

The observed activity aligns with common Discovery techniques defined by the MITRE ATT&CK framework.

No evidence of:

Privilege Escalation
Credential Dumping
Persistence
Lateral Movement
was observed during the investigation.

#### Recommendations
- Enable enhanced PowerShell logging
- Monitor PowerShell execution activity
- Alert on suspicious discovery commands
- Enable process creation auditing
- Review administrative group memberships

#### Lessons Learned

This investigation demonstrated how PowerShell can be used to perform host reconnaissance following initial access.
Monitoring PowerShell execution and child processes provides valuable visibility into attacker behavior and supports early detection of post-compromise activity.

