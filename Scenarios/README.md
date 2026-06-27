# Attack Scenarios

This directory contains the practical attack scenarios performed in the SOC lab environment.

The purpose of these scenarios is to demonstrate how Wazuh detects, logs, and correlates security events generated during different stages of an attack.

Each scenario includes:

* Scenario overview
* Attack execution
* Commands used
* Screenshots of the attack
* Wazuh detection and alerts
* Outcome

## Available Scenarios

* **Windows Scenario**

  * Service discovery using Nmap
  * Remote access through WinRM
  * PowerShell-based system enumeration
  * Detection using Wazuh

* **Ubuntu Scenario**

  * Web directory enumeration using Gobuster
  * Detection of repeated HTTP requests and discovered directories
  * Wazuh alert correlation

> **Note:** These scenarios were performed in a controlled lab environment for educational purposes. Some attack steps are simplified to demonstrate Wazuh's detection capabilities rather than simulate a complete real-world attack.
