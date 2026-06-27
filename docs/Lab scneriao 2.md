Windows machine scenario

This scenario demonstrates an end-to-end attack simulation performed in a controlled lab environment to evaluate Wazuh detection capabilities.

---

## Scenario Overview

A vulnerable Windows server was discovered exposed within the lab network during a reconnaissance phase. The service was identified through network scanning, revealing open management access.

Using available access credentials obtained during the simulation, the system was accessed remotely using a management tool. The objective was to simulate how an attacker could gain initial access and perform post-compromise activity.

---

## Post-Access Activity

After gaining access to the Windows machine, internal reconnaissance was performed to understand the environment.

This included:

- System information enumeration
- Network discovery from within the host
- User and process inspection

PowerShell commands were used to perform system-level enumeration, such as:

```powershell
Get-Process
Get-NetTCPConnection
Get-ComputerInfo
