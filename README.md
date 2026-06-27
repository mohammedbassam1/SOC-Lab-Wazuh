# SOC Lab - Wazuh Simulation

##  Overview
This project is a SOC (Security Operations Center) lab simulation built using Wazuh.  
It is designed to practice security monitoring, log analysis, endpoint detection, and attack simulation in a virtual environment.

---

## Lab Infrastructure

The lab environment consists of multiple virtual machines simulating a real-world SOC and attack scenario.

###  Machines

- **Ubuntu Server (SIEM)**
  - Acts as the central Wazuh SIEM

- **Kali Linux**
  - Used for attack simulation and testing

- **Windows 11**
  - Monitored endpoint with Sysmon and Wazuh agent

- **Ubuntu Server (Apache Web Server)**
  - Hosts a web service for monitoring and log collection

---

## Network Configuration

The lab uses **two network adapters** per virtual machine:

### 1. NAT Adapter
- Provides internet access for downloading tools and updates

### 2. Host-Only Adapter
- Used for internal communication between lab machines

---

## IP Addressing Scheme (Host-Only Network)

- Ubuntu SIEM (Wazuh): `192.168.56.1`
- Ubuntu Apache Server: `192.168.56.60`
- Kali Linux: `192.168.56.30`
- Windows 11: `192.168.56.40`

---

##  Setup Methodology

### 1. Virtualization
- Installed VirtualBox
- Created multiple virtual machines (Windows & Linux)
- Mounted ISO files for each operating system

### 2. Network Setup
- Configured NAT + Host-Only adapters for each VM
- Ensured all machines communicate through Host-Only network

### 3. IP Configuration
- Manually assigned static IPs for Linux machines
- Configured Windows 11 network adapter with static IP settings

### 4. Troubleshooting
- Some VMs were incorrectly configured with static NAT settings
- Fixed by reverting to DHCP for internet access when needed

---

## Purpose

- Build a realistic SOC environment
- Understand log collection and monitoring
- Simulate real-world attack scenarios
- Learn endpoint security monitoring (Windows & Linux)
- Practice SIEM operations using Wazuh

---

##  Key Features

- Centralized log collection using Wazuh
  
- Endpoint monitoring (Windows & Linux)
- Sysmon integration for Windows telemetry
- Apache web server log monitoring
- Attack simulation using Kali Linux
- Security event detection and analysis

---

## 🚀 Status

Completed as a functional SOC lab environment and continuously improved with additional detection scenarios and security testing.
