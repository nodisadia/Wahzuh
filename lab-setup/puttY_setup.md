# Week 1 Lab: PuTTY Setup for Ubuntu VM

## Learning Outcomes
- Download and install PuTTY on Windows
- Connect to Ubuntu VM via SSH using PuTTY
- Save session profile for quick access

## Objective
Configure PuTTY to remotely access the Ubuntu VM from Windows for command-line management.

## Prerequisites
- Ubuntu VM installed and running
- Ubuntu VM IP address (from `ip a` command)
- Ubuntu username and password (`wazuh-user`)
- OpenSSH server installed on Ubuntu

---

## Step 1: Download & Install PuTTY
```bash
1. Go to: https://www.putty.org/
2. Download putty.exe (64-bit)
3. Save to Desktop or Downloads folder
4. No installation needed - just double-click to run
```

## Step 2: Find Ubuntu VM IP Address
```bash
# Inside Ubuntu VM, run:
ip a

# Look for inet address under eth0 or ens33
# Example output:
# inet 192.168.1.100/24

# Your VM IP: _______________
```

## Step 3: Connect with PuTTY
```bash
1. Double-click putty.exe to open
2. Host Name: [enter your Ubuntu IP]
3. Port: 22
4. Connection type: SSH
5. Saved Sessions: Ubuntu-Wazuh
6. Click "Save"
7. Click "Open"
8. Click "Accept" if security alert appears
9. Login as: wazuh-user
10. Password: [type your password - it won't show]
```

## Step 4: Verify Connection
```bash
# After login, you should see:
wazuh-user@wazuh-server:~$

# Test commands:
whoami
# Output: wazuh-user

pwd
# Output: /home/wazuh-user

ip a
# Shows VM network info
```

## Step 5: Quick Reconnect (Saved Session)
```bash
1. Open PuTTY
2. Double-click "Ubuntu-Wazuh" from saved sessions
3. Login with your password
```

---

## Common Issues

| Problem | Fix |
|---------|-----|
| Connection refused | `sudo systemctl start ssh` in VM |
| Connection timeout | Check VM IP and Bridged network |
| Access denied | Verify username: wazuh-user |
| Can't find IP | Run `ip a` again in VM |

---

## Useful SSH Commands
```bash
# System info
uptime                 # How long VM has been running
free -h                # Check RAM usage
df -h                  # Check disk space

# File management
ls -la                 # List all files
cd /var/log            # Change directory
cat filename.txt       # View file content

# Service management
sudo systemctl status ssh   # Check SSH status
sudo systemctl restart ssh  # Restart SSH
```

---

## Verification Checklist
- [ ] PuTTY downloaded and opens
- [ ] Ubuntu VM is running
- [ ] Got IP address from `ip a`
- [ ] PuTTY connects successfully
- [ ] Can run commands on Ubuntu

---

**Setup Complete **
