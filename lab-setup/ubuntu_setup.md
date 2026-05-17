# Week 1 Lab: Installing Ubuntu on VirtualBox for Wazuh

## Learning Outcomes
- Create and configure a virtual machine in VirtualBox
- Manually install Ubuntu Server/Desktop
- Configure network settings (Bridged vs. NAT)
- Enable OpenSSH server for remote access
- Retrieve and document VM IP address

## Objective
Set up an Ubuntu virtual machine in VirtualBox as the host for Wazuh SIEM. The VM must be accessible from Windows via PuTTY and WinSCP.

## Prerequisites
- [VirtualBox](https://www.virtualbox.org/) installed
- Ubuntu 22.04 LTS ISO ([download](https://ubuntu.com/download/server))
- 8 GB RAM available on host
- 25 GB free disk space
![image alt ](https://github.com/nodisadia/Wahzuh/blob/bb1eadbd00edf8ce8ef27829450c87e0330f5fca/lab-setup/picture/Screenshot%202026-05-16%20183157.png)
---

## Step 1: Create Virtual Machine
```bash
1. Open VirtualBox → Click "New"
2. Name: Ubuntu-Wazuh
3. ISO: Select your Ubuntu ISO
4. ❌ Uncheck "Skip Unattended Installation"
5. Click "Next"
```
![image alt ](https://github.com/nodisadia/Wahzuh/blob/df36fc158d0241aa5c4ae244405ad9ed0639fc89/lab-setup/picture/Screenshot%202026-05-16%20183257.png)

## Step 2: Allocate Resources
| Setting | Value |
|---------|-------|
| RAM | 8192 MB (8 GB) |
| CPU | 2 cores |
| Disk | 25 GB (Dynamically allocated) |
![image alt ](https://github.com/nodisadia/Wahzuh/blob/df36fc158d0241aa5c4ae244405ad9ed0639fc89/lab-setup/picture/Screenshot%202026-05-16%20183444.png)
![image alt](https://github.com/nodisadia/Wahzuh/blob/df36fc158d0241aa5c4ae244405ad9ed0639fc89/lab-setup/picture/Screenshot%202026-05-16%20183730.png)
![image alt](https://github.com/nodisadia/Wahzuh/blob/df36fc158d0241aa5c4ae244405ad9ed0639fc89/lab-setup/picture/Screenshot%202026-05-16%20183830.png)

## Step 3: Configure Network
```bash
Settings → Network → Adapter 1
✅ Enable Network Adapter
Attached to: Bridged (for Windows access)
```
> ⚠️ **Bridged** = Windows can reach Ubuntu directly.  
> **NAT** = Requires port forwarding.

## Step 4: Install Ubuntu
```bash
1. Start the VM
2. Language: English
3. Installation type: Minimal
4. Storage: Entire disk
5. Profile:
   - Name: Wazuh User
   - Computer: wazuh-server
   - Username: wazuh-user
   - Password: [choose strong password]
6. ✅ CHECK "Install OpenSSH server"
7. Skip featured snaps
8. Click "Install"
```
![image alt](https://github.com/nodisadia/Wahzuh/blob/df36fc158d0241aa5c4ae244405ad9ed0639fc89/lab-setup/picture/Screenshot%202026-05-16%20184913.png)
![image alt ](https://github.com/nodisadia/Wahzuh/blob/df36fc158d0241aa5c4ae244405ad9ed0639fc89/lab-setup/picture/Screenshot%202026-05-16%20183908.png)
![image alt ](https://github.com/nodisadia/Wahzuh/blob/df36fc158d0241aa5c4ae244405ad9ed0639fc89/lab-setup/picture/Screenshot%202026-05-16%20184021.png)
![image alt ](https://github.com/nodisadia/Wahzuh/blob/df36fc158d0241aa5c4ae244405ad9ed0639fc89/lab-setup/picture/Screenshot%202026-05-16%20185140.png)
![image alt ](https://github.com/nodisadia/Wahzuh/blob/df36fc158d0241aa5c4ae244405ad9ed0639fc89/lab-setup/picture/Screenshot%202026-05-16%20185223.png)
![image alt ](https://github.com/nodisadia/Wahzuh/blob/df36fc158d0241aa5c4ae244405ad9ed0639fc89/lab-setup/picture/Screenshot%202026-05-16%20185300.png)
![image alt ](https://github.com/nodisadia/Wahzuh/blob/df36fc158d0241aa5c4ae244405ad9ed0639fc89/lab-setup/picture/Screenshot%202026-05-16%20185311.png)
![image alt ](https://github.com/nodisadia/Wahzuh/blob/df36fc158d0241aa5c4ae244405ad9ed0639fc89/lab-setup/picture/Screenshot%202026-05-16%20185326.png)
![image alt ](https://github.com/nodisadia/Wahzuh/blob/df36fc158d0241aa5c4ae244405ad9ed0639fc89/lab-setup/picture/Screenshot%202026-05-16%20185414.png)
![image alt ](https://github.com/nodisadia/Wahzuh/blob/df36fc158d0241aa5c4ae244405ad9ed0639fc89/lab-setup/picture/Screenshot%202026-05-16%20185655.png)
![image alt ](https://github.com/nodisadia/Wahzuh/blob/df36fc158d0241aa5c4ae244405ad9ed0639fc89/lab-setup/picture/Screenshot%202026-05-16%20185706.png)
![image alt ](https://github.com/nodisadia/Wahzuh/blob/df36fc158d0241aa5c4ae244405ad9ed0639fc89/lab-setup/picture/Screenshot%202026-05-16%20185718.png)
![image alt ](https://github.com/nodisadia/Wahzuh/blob/df36fc158d0241aa5c4ae244405ad9ed0639fc89/lab-setup/picture/Screenshot%202026-05-16%20185744.png)
![image alt ](https://github.com/nodisadia/Wahzuh/blob/fd876375f599dbbe05cb94141464a654f227cf34/lab-setup/picture/Screenshot%202026-05-16%20185950.png)
![image alt ](https://github.com/nodisadia/Wahzuh/blob/fd876375f599dbbe05cb94141464a654f227cf34/lab-setup/picture/Screenshot%202026-05-16%20190113.png)
![image alt ](https://github.com/nodisadia/Wahzuh/blob/fd876375f599dbbe05cb94141464a654f227cf34/lab-setup/picture/Screenshot%202026-05-16%20190202.png)
![image alt ](https://github.com/nodisadia/Wahzuh/blob/fd876375f599dbbe05cb94141464a654f227cf34/lab-setup/picture/Screenshot%202026-05-16%20190358.png)
![image alt ](https://github.com/nodisadia/Wahzuh/blob/fd876375f599dbbe05cb94141464a654f227cf34/lab-setup/picture/Screenshot%202026-05-16%20190412.png)
![image alt ](https://github.com/nodisadia/Wahzuh/blob/fd876375f599dbbe05cb94141464a654f227cf34/lab-setup/picture/Screenshot%202026-05-16%20190449.png)
![image alt ](https://github.com/nodisadia/Wahzuh/blob/fd876375f599dbbe05cb94141464a654f227cf34/lab-setup/picture/Screenshot%202026-05-16%20192221.png)
![image alt ](https://github.com/nodisadia/Wahzuh/blob/fd876375f599dbbe05cb94141464a654f227cf34/lab-setup/picture/Screenshot%202026-05-16%20192347.png)
## Step 5: First Boot
```bash
1. Click "Reboot" when finished
2. Press Enter if asked to remove installation medium
3. Log in with: wazuh-user / [your password]
```

## Step 6: Verify IP Address
```bash
ip a
```
Look for IP address (e.g., `192.168.x.x`). Save this for PuTTY/WinSCP.

---
![image alt ](https://github.com/nodisadia/Wahzuh/blob/fd876375f599dbbe05cb94141464a654f227cf34/lab-setup/picture/Screenshot%202026-05-16%20192753.png)

## Verification Checklist
- [ ] VM boots successfully
- [ ] Can log in with `wazuh-user`
- [ ] `ip a` shows an IP address
- [ ] Can ping VM from Windows (optional)

## Next Steps
- Connect via PuTTY using the VM's IP address
- Transfer files with WinSCP
- Begin Wazuh installation

---

**Lab Complete **
```
