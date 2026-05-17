## Learning Outcomes
- Download and install WinSCP on Windows
- Connect to Ubuntu VM via SFTP
- Transfer files between Windows and Ubuntu
- Edit remote files directly

## Objective
Configure WinSCP to securely transfer files between Windows and Ubuntu VM for managing configuration files, logs, and scripts.

## Prerequisites
- Ubuntu VM installed and running
- Ubuntu VM IP address (from `ip a` command)
- Ubuntu username and password (`wazuh-user`)
- OpenSSH server installed on Ubuntu

---

## Step 1: Download & Install WinSCP

```bash
1. Go to: https://winscp.net/
2. Click green "Download WinSCP" button
3. Run the installer
4. Choose "Typical installation"
5. Interface: "Commander" (dual-panel)
6. Click "Install" → "Finish"
```
![image alt](https://github.com/nodisadia/Wahzuh/blob/4488c13a450f78a22af652d18ac4f3f6c08c1474/lab-setup/picture/Screenshot%202026-05-17%20140325.png)
---

## Step 2: Find Ubuntu VM IP Address

```bash
# Inside Ubuntu VM, run:
ip a | grep inet

# Look for inet address under eth0 or ens33
# Example: inet 192.168.1.100/24

# Your VM IP: _______________
```

---

## Step 3: Create WinSCP Session

```bash
1. Open WinSCP
2. File protocol: SFTP
3. Host name: [your Ubuntu IP]
4. Port number: 22
5. User name: wazuh-user
6. Password: [your password]
7. Click "Save"
8. Name: Ubuntu-Wazuh
9. Click "OK"
10. Click "Login"
11. Click "Accept" if security alert appears
```

---

## Step 4: Navigate the Interface

```bash
# Left Panel = Windows (local)
# Right Panel = Ubuntu (remote)

# Common locations:
Windows paths:
- Desktop: C:\Users\YourName\Desktop
- Downloads: C:\Users\YourName\Downloads

Ubuntu paths:
- Home: /home/wazuh-user/
- Config: /etc/
- Logs: /var/log/
```
![image alt](https://github.com/nodisadia/Wahzuh/blob/4488c13a450f78a22af652d18ac4f3f6c08c1474/lab-setup/picture/Screenshot%202026-05-17%20141032.png)
![image alt](https://github.com/nodisadia/Wahzuh/blob/4488c13a450f78a22af652d18ac4f3f6c08c1474/lab-setup/picture/Screenshot%202026-05-17%20141042.png)
![image alt](https://github.com/nodisadia/Wahzuh/blob/4488c13a450f78a22af652d18ac4f3f6c08c1474/lab-setup/picture/Screenshot%202026-05-17%20141053.png)
---

## Step 5: Transfer Files

### Transfer Single File
```bash
1. Select file in left panel (Windows)
2. Drag to right panel (Ubuntu)
3. Click "Copy"
4. File appears in /home/wazuh-user/
```

### Transfer Folder
```bash
1. Select folder in Windows panel
2. Drag to Ubuntu panel
3. Click "Copy"
4. Entire folder transfers with structure
```

### Download from Ubuntu to Windows
```bash
1. Select file in right panel (Ubuntu)
2. Drag to left panel (Windows)
3. Click "Copy"
```

---
![image alt](https://github.com/nodisadia/Wahzuh/blob/4488c13a450f78a22af652d18ac4f3f6c08c1474/lab-setup/picture/Screenshot%202026-05-17%20141534.png)
![image alt](https://github.com/nodisadia/Wahzuh/blob/4488c13a450f78a22af652d18ac4f3f6c08c1474/lab-setup/picture/Screenshot%202026-05-17%20141544.png)
## Step 6: Edit Remote Files

```bash
1. Right-click file in Ubuntu panel
2. Click "Edit"
3. File opens in Notepad
4. Make changes
5. Save and close
6. WinSCP asks to upload → Click "Yes"
```

---





**Setup Complete **
