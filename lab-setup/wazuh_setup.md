# Week 3 Lab: Installing Wazuh SIEM on Ubuntu

## Learning Outcomes
By the end of this lab, you will be able to:

- Install Wazuh all-in-one (Manager + Indexer + Dashboard) on Ubuntu  
- Configure Wazuh Indexer (OpenSearch) with secure authentication  
- Set up Wazuh Dashboard with admin credentials  
- Open necessary firewall ports for web access and agent communication  
- Access the Wazuh Dashboard from a Windows browser  
- Verify all Wazuh services are running correctly  

## Objective
Deploy a fully functional Wazuh SIEM platform on the Ubuntu VM created in Week 1. Wazuh will provide security monitoring, intrusion detection, log analysis, and vulnerability detection capabilities. The installation will be accessible via web browser from your Windows machine for ongoing security operations.

## Scenario
Your organization needs an open-source SIEM solution to centralize security event monitoring. You have been tasked with deploying Wazuh in a lab environment before production rollout. The Wazuh server must collect logs from endpoints, provide a web-based dashboard for analysis, and support future agent deployments. You will use PuTTY to run the installation commands and WinSCP to transfer any configuration files if needed.

## Prerequisites

- Ubuntu VM from **Week 1 Lab** (running, with internet access)  
- PuTTY from **Week 2 Lab** (to run commands)  
- Ubuntu VM IP address (e.g., `192.168.1.100`)  
- Ubuntu user with `sudo` privileges (e.g., `wazuh-user`)  
- At least 4 GB RAM free on Ubuntu VM (8 GB recommended)  
- Port 443 accessible from Windows (not blocked by firewall)

---

## Part 1: Prepare Ubuntu for Wazuh Installation

### Step 1: Connect to Ubuntu via PuTTY

1. Open **PuTTY**.
2. Load your saved `Ubuntu-Wazuh` session.
3. Click **Open**.
4. Login with your username and password.

### Step 2: Update System Packages

Run the following commands:

```bash
sudo apt update && sudo apt upgrade -y
## Step-by-Step: Install Wazuh on Ubuntu via PuTTY

###  1. Connect using PuTTY

- Open PuTTY
- Enter:
  - **Host Name:** `your_server_ip`
  - **Port:** `22`
- Click **Open**

Login with:
- username
- password

###  2. Update your system

Run:

```bash
sudo apt update && sudo apt upgrade -y
```

### 3. Install required packages

```bash
sudo apt install curl apt-transport-https unzip wget -y
```

### 4. Download Wazuh installation script

```bash
curl -sO https://packages.wazuh.com/4.7/wazuh-install.sh
```

###  5. Make script executable

```bash
chmod +x wazuh-install.sh
```

###  6. Run installation (All-in-One setup)

This installs:
- Wazuh Manager
- Wazuh Dashboard
- Elasticsearch (Indexer)

```bash
sudo ./wazuh-install.sh -a
```

 This may take 10–20 minutes.

###  7. Get login credentials

After installation:

```bash
sudo tar -xvf wazuh-install-files.tar
```

Then check:

```bash
cat wazuh-install-files/wazuh-passwords.txt
```

You'll see:

```
Username: admin
Password: (generated)
```

### 8. Access Wazuh Dashboard

Open browser:

```
https://your_server_ip
```

 You may see a security warning → click **Advanced** → **Proceed**

###  9. Enable services (optional check)

```bash
sudo systemctl status wazuh-manager
sudo systemctl status wazuh-dashboard
```

---

## Common Issues (Important)

###  Port blocked

Make sure firewall allows:

```bash
sudo ufw allow 443
sudo ufw allow 1514
sudo ufw allow 1515
```

###  Low RAM

Wazuh needs at least:
- **4 GB RAM** (minimum)
- **8 GB** recommended

---

If your server is weak (like a small VPS), don't use `-a`. Instead install only the manager:

```bash
sudo ./wazuh-install.sh -s
```

![image alt](https://github.com/nodisadia/Threat-Model-Lab/blob/c79a35de7f865d73243133c9586bcbff72eaa751/lab-setup/picture/Screenshot%202026-05-17%20195823.png)
