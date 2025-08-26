# WAZUH-SIEM-LAB
Hands-on SIEM project built with Wazuh, Ubuntu server, and agent VMs in VirtualBox. Logs collected, alerts generated, and dashboard monitoring tested.

# WAZUH-SIEM-LAB  

Hands-on SIEM project built with **Wazuh**, using an Ubuntu server and an Ubuntu agent inside VirtualBox.  
This lab demonstrates how logs are collected, alerts generated, and security events mapped to MITRE ATT&CK.  

---

## 📌 Project Overview  
The goal of this lab was to gain hands-on experience deploying and operating a **Security Information and Event Management (SIEM)** system.  
I built a **Wazuh server** and connected an **Ubuntu agent VM**, then generated and analyzed events to verify endpoint monitoring.  

This project simulates how a SOC team would deploy agents across endpoints and centralize logs into a SIEM for monitoring and investigation.  

---

## ⚙️ Lab Environment  
- **Hypervisor**: Oracle VirtualBox  
- **Wazuh Server**: Ubuntu 24.04 LTS (`10.0.2.15`)  
- **Wazuh Agent**: Ubuntu 24.04 LTS (`10.0.2.4`)  
- **Wazuh Version**: v4.12.0  
- **Browser**: Firefox (for dashboard access)  

---

## 🛠️ Steps Performed  
1. Installed **Wazuh Manager + Dashboard** on the server VM.  
2. Installed the **Wazuh Agent** on a second Ubuntu VM.  
3. Edited the `ossec.conf` file to point the agent at the server’s IP.  
4. Registered the agent using `manage_agents`, extracted the key, and authenticated with the server.  
5. Generated logs and events:  
   - Ran `sudo` commands to trigger privilege escalation alerts.  
   - Created test files (e.g., `wazuh_test.txt`) to confirm file monitoring.  
6. Verified events in the **Wazuh Dashboard** (Threat Hunting, MITRE ATT&CK, Compliance tabs).  

---

## 📊 Results & Analysis  
✅ Agent successfully registered and appeared **Active** in the dashboard.  
✅ Logs collected included:  
- `Successful sudo to ROOT executed`  
- `PAM: Login session opened/closed`  
✅ MITRE ATT&CK mappings included tactics like:  
- Privilege Escalation  
- Defense Evasion  
- Persistence  

This showed how Wazuh correlates real system activity to security tactics/techniques.  

---

## ⚠️ Challenges Faced  

This was **not a smooth, one-click install** — I had to troubleshoot multiple issues along the way:  

1. **VM Networking Issues**  
   - At first, the server and agent could not communicate.  
   - Fixed by adjusting VirtualBox network settings (NAT Adapter + Host-only, same subnet).  

2. **Agent Connection Failures**  
   - Got repeated errors like `ERROR: Unable to add agent (from manager)` and `Duplicate agent name`.  
   - Resolved by removing duplicate agents in `manage_agents` and re-registering with a fresh key.  

3. **Permission Problems**  
   - Couldn’t read `ossec.conf` or run certain commands at first due to permissions.  
   - Solved by using `sudo` properly (ex: `sudo grep address /var/ossec/etc/ossec.conf`).  

4. **Wazuh Install Hurdles**  
   - Initial Wazuh install failed because of missing dependencies and version mismatches.  
   - After researching docs and forums, re-installed using the official Wazuh installation script which fixed it.  

Each of these issues forced me to **dig into logs, configs, and documentation** — which made the project more valuable than just a clean install.  

---

## 🚀 Key Takeaways  
- Learned how to deploy and configure a SIEM in a realistic lab environment.  
- Practiced **debugging agent/server communication issues**.  
- Experienced how Wazuh maps real activity (sudo, login sessions) into **alerts + MITRE ATT&CK tactics**.  
- Understood the importance of **proper networking and config management** in SIEM deployments.  

