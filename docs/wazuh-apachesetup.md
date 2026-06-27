# .Install Apache on Ubuntu (Web Server)

On your Ubuntu machine:

```
sudo apt updatesudo apt install apache2 -y
```


Enable and start it:

```
sudo systemctl enable apache2sudo systemctl start apache2
```

Check status:

```
sudo systemctl status apache2
```

Test locally:

```
curl http://localhost
```


We added some panels and pages   so we can simulate some attacks

now we configure the apache logs

#  Make Apache log MORE useful (IMPORTANT)

Edit Apache config:

```
sudo nano /etc/apache2/apache2.conf
```

Find or ensure this exists:

```
LogFormat "%h %l %u %t \"%r\" %>s %b \"%{User-agent}i\"" combinedCustomLog ${APACHE_LOG_DIR}/access.log combined
```

👉 This ensures logs include:

- IP address
- request path
- status code
- user-agent (VERY important for SOC)



# 3. Enable “Security-style logging” (better for SOC)

Upgrade log format:

```
LogFormat "%h %t \"%r\" %>s %b \"%{Referer}i\" \"%{User-agent}i\" %D" securityCustomLog ${APACHE_LOG_DIR}/access.log security
```

Now logs include:

- response time (`%D`)
- referrer
- user agent
- request details

👉 This is what SOC analysts love


## Restart Apache after changes

```
sudo systemctl restart apache2
```




# INSTALLING agent 



## STEP 1 — Add Wazuh repo (Ubuntu)

On the Ubuntu Apache machine:

```
curl -s https://packages.wazuh.com/key/GPG-KEY-WAZUH | sudo gpg --dearmor -o /usr/share/keyrings/wazuh.gpg
```

```
echo "deb [signed-by=/usr/share/keyrings/wazuh.gpg] https://packages.wazuh.com/4.x/apt/ stable main" | sudo tee /etc/apt/sources.list.d/wazuh.list
```

```
sudo apt update
```



# 📦 STEP 2 — Install Wazuh agent



```
sudo apt install wazuh-agent -y
```


# STEP 3— Point agent to your Wazuh manager

Edit config:

```
sudo nano /var/ossec/etc/ossec.conf
```


Find this section:

```
<server>  <address>MANAGER_IP</address></server>
```

Replace:

```
<server>  <address>YOUR_WAZUH_MANAGER_IP</address></server>
```


#  STEP 4 — Register agent with manager

On Wazuh manager:

```
/var/ossec/bin/manage_agents
```

- Press `A` → Add agent
- Give name: `apache-ubuntu`
- Set IP: Ubuntu machine IP
- Copy generated key

# STEP 5 — Import key on Ubuntu agent

On Ubuntu  apache server :

```
/var/ossec/bin/manage_agents
```

Then:

- Press `I` → Import key
- Paste key from manager
- Confirm

# STEP 6 — Start agent

```
sudo systemctl enable wazuh-agentsudo systemctl restart wazuh-agent
```


# 📡 STEP 7 — Ensure  logs are collected

```
sudo nano /var/ossec/etc/ossec.conf
```

<!-- Apache access logs -->
<localfile>
  <log_format>apache</log_format>
  <location>/var/log/apache2/access.log</location>
</localfile>

<!-- Apache error logs -->
<localfile>
  <log_format>apache</log_format>
  <location>/var/log/apache2/error.log</location>
</localfile>

<!-- Authentication logs (SSH, sudo, login attempts) -->
<localfile>
  <log_format>syslog</log_format>
  <location>/var/log/auth.log</location>
</localfile>

<!-- General system logs -->
<localfile>
  <log_format>syslog</log_format>
  <location>/var/log/syslog</location>
</localfile>

<!-- Kernel / system security events -->
<localfile>
  <log_format>syslog</log_format>
  <location>/var/log/kern.log</location>
</localfile>



Restart again:

```
sudo systemctl restart wazuh-agent
