 # SOC Lab Attack Scenarios

This document describes the attack simulations performed in the lab and how Wazuh detected and generated alerts from them.

---


## Scenario 2: Windows Powershell access (kali -Evilwinrm)


on terminal 
```
nmap 192.168.56.40
```

![nmap scan](images/nmapWin.png)


The scan results revealed two exposed services on the target Windows machine:

- 5357/tcp (WSDAPI) — Windows device discovery service, not relevant for exploitation  
- 5985/tcp (WinRM) — Windows Remote Management service used for remote PowerShell access


Using valid credentials (username and password), access to the Windows machine was established through the exposed WinRM service (port 5985).

A remote PowerShell session was initiated, allowing interaction with the system from the Kali Linux machine.

![access](images/accessingpowershell.png)

