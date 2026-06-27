


### Check interfaces:
```
ip a
```



### Check routing table:


```
ip route
```



### Add IP manually (host-only):

```
sudo ip addr add 192.168.56.30/24 dev eth1
```



### Bring interface up:

```
sudo ip link set eth1 up

```


### Add default route (NAT internet):

```
sudo ip route add default via 10.0.2.2
```


### Ping test:

```
ping 192.168.56.40
```


### Network scan (discover devices):

```
nmap -sn 192.168.56.0/24
```


### Scan Windows ports (SMB/NetBIOS):

```
nmap -sS -p 135,139,445 192.168.56.40
```


### NetBIOS scan:

```
nbtscan 192.168.56.0/24
```

========================================
WINDOWS COMMANDS
========================================

### Check IP:

```
ipconfig
```


### Full network info:

```
ipconfig /all
```

 ### Ping
 ```
ping 192.168.56.30
```


### Enable ICMP (ping):

```
netsh advfirewall firewall add rule name="Allow ICMPv4-In" protocol=icmpv4:8,any dir=in action=allow
```


### Firewall ON/OFF:

```
netsh advfirewall set allprofiles state on
netsh advfirewall set allprofiles state off
```

---

 ### List all running services

```
net start
```

 Shows only services that are currently running.

---

### for More detailed list (all services + state)

```
sc query type= service state= all
```

---

### to Filter services (still general, not specific)

Example: show anything related to “wazuh”

```
sc query type= service state= all | findstr /i wazuh
```


========================================
NETWORK MANAGER (LINUX GUI)
========================================

###  run Command in Terminal :
nmtui

Inside nmtui:
- Edit a connection
- Set DHCP for NAT (eth0)
- Set Manual for host-only (eth1)
- IP example: 192.168.56.60/24
- Gateway: (empty for host-only)

Activate connection:
- Activate a connection


========================================
VIRTUALBOX SETUP
========================================

Adapter 1: NAT (internet)
Adapter 2: Host-only (lab network)



## Notes:

in linux   

while using commands like :

`sudo ip link set eth1 up , sudo ip route add default via 10.0.2.2`

applied changes will be removed  after  reboot   so for persistent changes use either network manager (nmtui)  in terminal or go to settings and network connections


In windows changing IP from network adapters  will automatically be persistent 


Think of it like this:

- `ip link / ip route` = “change it live in RAM”
- config files = “save it for future boots”
