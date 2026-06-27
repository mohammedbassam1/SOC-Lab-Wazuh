# Windows 11 setup  from sysmon / configuring wazuh agent


## we start by installing sysmon 


https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon  from here  u download sysmon 


then u  download sysmon config file 

https://github.com/SwiftOnSecurity/sysmon-config  and put it inside sysmon folder


then u open cmd admin inside the sysmon file

and start it  install

`sysmon.exe -accepteula -i sysmonconfig-export.xml`


### Update existing configuration

[](https://github.com/SwiftOnSecurity/sysmon-config?utm_source=chatgpt.com#update-existing-configuration)

Run with administrator rights

```
sysmon.exe -c sysmonconfig-export.xml
```

### Uninstall

[](https://github.com/SwiftOnSecurity/sysmon-config?utm_source=chatgpt.com#uninstall)

Run with administrator rights

```
sysmon.exe -u
```




## Confirm Sysmon is working
 

Run on Windows CMD :  

```
sc query sysmon64
```

You want:

- `STATE: RUNNING`

---

 Check logs locally (VERY IMPORTANT)
 
Open event viewer

```
Event Viewer → Applications and Services Logs → Microsoft → Windows → Sysmon → Operational
```




## Installing WAZUH AGENT

1. Download the [Windows installer](https://packages.wazuh.com/4.x/windows/wazuh-agent-4.14.5-1.msi) to start the installation process. from this page (wazuh agent install page  )
2. 
https://documentation.wazuh.com/current/installation-guide/wazuh-agent/wazuh-agent-package-windows.html

2 - open the wazuh-agent GUI:

and put the wazuh manager IP  192.168.56.1


By default, all agent files are stored in `C:\Program Files (x86)\ossec-agent` after the installation.


## To verify its connected    


-go to Wazuh dashboard   and check agent management  



OR

-in  the Windows Machine CMD

```
sc query WazuhSvc

```


   if u wanna  Restart Wazuh Agent
```
net stop WazuhSvc
net start WazuhSvc
```



# How we configured log collection on the Windows VM (Wazuh Agent)

We configured the Wazuh agent on the Windows 11 VM to define which logs should be collected and sent to the Wazuh manager for SIEM monitoring.

---

## 🧩 1. File used for configuration

We edited the Wazuh agent configuration file on the Windows machine:

```
C:\Program Files (x86)\ossec-agent\ossec.conf
```

This file controls what logs the agent collects locally.

---

## ⚙️ 2. Log sources we enabled

Inside `ossec.conf`, we added multiple `<localfile>` blocks to define Windows Event Log channels.

---

### 🔐 Security logs (authentication & system access)

```
<localfile>  <location>Security</location>  <log_format>eventchannel</log_format></localfile>
```

✔ Collects:

- Login success (4624)
- Login failure (4625)
- Account access events

---

### ⚡ Sysmon logs (process & system activity)

```
<localfile>  <location>Microsoft-Windows-Sysmon/Operational</location>  <log_format>eventchannel</log_format></localfile>
```

✔ Collects:

- Process creation (Event ID 1)
- Network connections (Event ID 3)
- File creation (Event ID 11)

---

### 🧠 PowerShell logs (command execution)

```
<localfile>  <location>Microsoft-Windows-PowerShell/Operational</location>  <log_format>eventchannel</log_format></localfile>
```

✔ Collects:

- PowerShell execution events
- Script activity (including advanced logging if enabled)

---

### 📦 Application logs

```
<localfile>  <location>Application</location>  <log_format>eventchannel</log_format></localfile>
```

✔ Collects:

- Application errors
- Software installation events
- Program activity logs

---

## 🔄 3. Applying the configuration

After editing the file, we restarted the Wazuh agent service to apply changes:

```
net stop WazuhSvcnet start WazuhSvc
```

or:

```
Restart-Service WazuhSvc
```



# PowerShell Logging Configuration (What we did on the VM)

We enabled PowerShell logging features to improve visibility of command execution and script activity on the Windows 11 VM.

---

# ⚙️ 1. Registry commands used (enabling logging)

We created and enabled PowerShell logging policies using PowerShell commands.

---

## 🧠 Script Block Logging (MOST IMPORTANT)

```
New-Item -Path "HKLM:\Software\Policies\Microsoft\Windows\PowerShell\ScriptBlockLogging" -Force

Set-ItemProperty -Path "HKLM:\Software\Policies\Microsoft\Windows\PowerShell\ScriptBlockLogging" -Name EnableScriptBlockLogging -Value 1
```

✔ Captures PowerShell commands (Event ID 4104)

---

## 🧠 Module Logging

```
New-Item -Path "HKLM:\Software\Policies\Microsoft\Windows\PowerShell\ModuleLogging" -Force

Set-ItemProperty -Path "HKLM:\Software\Policies\Microsoft\Windows\PowerShell\ModuleLogging" -Name EnableModuleLogging -Value 1
```

✔ Captures PowerShell module usage

---

## 🧠 Transcription logging

```
New-Item -Path "HKLM:\Software\Policies\Microsoft\Windows\PowerShell\Transcription" -Force

Set-ItemProperty -Path "HKLM:\Software\Policies\Microsoft\Windows\PowerShell\Transcription" -Name EnableTranscripting -Value 1
```

✔ Records full PowerShell session output

---

# 🔄 2. Commands used to apply changes

After enabling logging, we ensured services and system updates applied the configuration.

```
Restart-Service WazuhSvc
```




installing atomic red team to test attacks

from git hub 

https://github.com/redcanaryco/atomic-red-team download the zip file  u might need to turn of the firewall on the VM




Configuring RDP  on windows 11
