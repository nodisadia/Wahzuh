Nodi
nodi_sadia__
In a call

PsycHE [CAT],  — 5:38 PM
?????????????
fsdhsdhsetjgfjrsse
gh kfxi
koiiiiiiiiiii
amar sesh
Nodi [CAT],  — 5:41 PM
koi
Nodi [CAT],  — 5:54 PM
koi
You missed a call from 
PsycHE
 that lasted 3 minutes. — 7:22 PM
PsycHE [CAT],  — 7:22 PM
@Nodi
Nodi
 started a call. — 7:31 PM
PsycHE [CAT],  — 7:40 PM
# Week 3 Lab: Log Analysis with CLI Tools (SSH Brute-Force Investigation)

## Learning Outcomes
By the end of this lab, you will be able to:

- Use `grep` with regular expressions to detect authentication failures

message.txt
8 KB
                                                                                                                                              
# Week 3 Lab: Log Analysis with CLI Tools (SSH Brute-Force Investigation)

## Learning Outcomes
By the end of this lab, you will be able to:

- Use `grep` with regular expressions to detect authentication failures
- Utilize `awk` to extract timestamps, IP addresses, and usernames from logs
- Employ `sed` to sanitize and transform log entries for reporting
- Chain commands (`cut`, `sort`, `uniq`, `wc`, `head`, `tail`) for data aggregation
- Identify brute-force attack patterns in `/var/log/auth.log`
- Create a professional incident report with statistics and evidence

## Objective
Master Linux command-line tools to analyze authentication logs and detect a simulated SSH brute-force attack. You will generate a forensic report identifying attack sources, targeted usernames, and attack timelines.

## Scenario
You are a junior SOC analyst at CyberDefend Corp. Overnight, the intrusion detection system triggered an alert for "Multiple Failed SSH Logins" on a critical Ubuntu server. Your task is to analyze `/var/log/auth.log` (or a sample provided) to:

- Determine if a brute-force attack occurred
- Identify the attacker's IP address(es)
- List which usernames were targeted
- Calculate the attack duration and frequency
- Provide evidence for the incident report

## Prerequisites

- Linux system (Ubuntu VM from Week 2, or any Debian-based distribution)
- Basic familiarity with terminal commands
- Sample log file (`auth.log` or simulated brute-force log)
- Text editor for report writing

## Lab Duration
Approximately 2-3 hours

---

## Part 1: Understanding SSH Authentication Logs (15 minutes)

### Step 1: Auth.log Format Overview

On Ubuntu/Debian systems, SSH authentication events are logged to `/var/log/auth.log`. A typical failed SSH login looks like this:

```
Mar 10 04:32:15 ubuntu-server sshd[12456]: Failed password for root from 192.168.1.100 port 54321 ssh2
```

A successful login:

```
Mar 10 04:32:20 ubuntu-server sshd[12456]: Accepted password for john from 192.168.1.101 port 54322 ssh2
```

Other important event types:

| Event Type | Log Pattern |
|------------|--------------|
| Invalid user | `Invalid user` |
| Failed password | `Failed password` |
| Accepted password | `Accepted password` |
| Connection closed | `Connection closed` |
| Disconnected | `Disconnected` |

### Step 2: Prepare Your Log File

Create a working directory and obtain a sample log:

```bash
mkdir -p ~/soc-labs/week3-ssh
cd ~/soc-labs/week3-ssh
```

**Option 1 – Use real system log (if you have SSH failures):**

```bash
sudo cp /var/log/auth.log .
sudo chown $USER:$USER auth.log
```

**Option 2 – Download a simulated brute-force log:**

```bash
wget https://raw.githubusercontent.com/linux-audit/audit-documentation/main/sample-logs/auth-bruteforce.log -O auth.log
```

**Option 3 – Generate your own simulated log (if wget fails):**

```bash
cat > auth.log << 'EOF'
Mar 10 04:15:22 server sshd[12345]: Failed password for root from 203.0.113.5 port 45012 ssh2
Mar 10 04:15:25 server sshd[12346]: Failed password for admin from 203.0.113.5 port 45013 ssh2
Mar 10 04:15:28 server sshd[12347]: Failed password for root from 203.0.113.5 port 45014 ssh2
Mar 10 04:15:31 server sshd[12348]: Failed password for admin from 203.0.113.5 port 45015 ssh2
Mar 10 04:15:34 server sshd[12349]: Failed password for root from 203.0.113.5 port 45016 ssh2
Mar 10 04:15:37 server sshd[12350]: Failed password for ubuntu from 203.0.113.5 port 45017 ssh2
Mar 10 04:16:02 server sshd[12351]: Failed password for root from 198.51.100.88 port 33001 ssh2
Mar 10 04:16:05 server sshd[12352]: Failed password for root from 198.51.100.88 port 33002 ssh2
Mar 10 04:16:08 server sshd[12353]: Failed password for root from 198.51.100.88 port 33003 ssh2
Mar 10 04:20:30 server sshd[12400]: Accepted password for legitimate-user from 192.168.1.50 port 52001 ssh2
EOF
```

Verify the file:

```bash
cat auth.log
```

---

## Part 2: Basic Log Analysis (30 minutes)

### Exercise 1: Count Total Authentication Events

**Question:** How many total authentication-related events are in the log?

**Command:**

```bash
wc -l auth.log
```

**Explanation:**
- `wc` = word count command
- `-l` = count lines (each line = one event)

**Document:** Record the total number in your report.

---

### Exercise 2: Extract Failed Password Attempts

**Question:** How many failed password attempts occurred?

**Command:**

```bash
grep "Failed password" auth.log | wc -l
```

**Explanation:**
- `grep "Failed password"` = filter lines containing that exact phrase
- `| wc -l` = count matching lines

**Alternative using `-c` flag:**

```bash
grep -c "Failed password" auth.log
```

**Expected output (for sample):** `7`

---

### Exercise 3: Identify Attacker IP Addresses

**Question:** What are the unique IP addresses that generated failed logins?

**Step-by-step approach:**

1. Extract the IP address field (varies by log format – typically the 11th field or after "from"):

```bash
grep "Failed password" auth.log | awk '{print $11}'
```

> **Note:** Depending on your log format, the IP might be in `$11`, `$12`, or `$14`. Adjust as needed.

2. Sort the IPs:

```bash
grep "Failed password" auth.log | awk '{print $11}' | sort
```

3. Remove duplicates:

```bash
grep "Failed password" auth.log | awk '{print $11}' | sort -u
```

**Expected output (for sample):**

```
198.51.100.88
203.0.113.5
```

**Document:** List all attacker IPs in your report.

---

### Exercise 4: Find Top Attackers (Frequency)

**Question:** Which IP address attempted the most failed logins?

**Command:**

```bash
grep "Failed password" auth.log | awk '{print $11}' | sort | uniq -c | sort -rn | head -5
```

**Breakdown:**

| Command piece | Purpose |
|---------------|---------|
| `awk '{print $11}'` | Extract IP address |
| `sort` | Group identical IPs together |
| `uniq -c` | Count occurrences of each IP |
| `sort -rn` | Sort by count (reverse/numerical) |
| `head -5` | Show top 5 results |

**Expected output (for sample):**

```
      5 203.0.113.5
      3 198.51.100.88
```

**Analysis:** High frequency from a single IP indicates brute-force scanning.

---

### Exercise 5: Identify Targeted Usernames

**Question:** Which usernames were most frequently targeted?

**Command:**

```bash
grep "Failed password" auth.log | awk '{print $9}' | sort | uniq -c | sort -rn
```

> **Note:** Adjust field number (`$9` or `$11`) based on your log format. In the sample, username is the 9th field (e.g., "for root" → `$9` = "root").

**Expected output (for sample):**

```
      5 root
      2 admin
      1 ubuntu
```

**Security Insight:** Attackers always try `root` first, then common admin names.

---

## Part 3: Advanced Pattern Matching (45 minutes)

### Exercise 6: Detect Invalid User Attempts

**Question:** How many attempts used non-existent usernames?

**Command:**

```bash
grep "Invalid user" auth.log | wc -l
```

**View the actual invalid usernames:**

```bash
grep "Invalid user" auth.log | awk '{print $8}' | sort | uniq -c
```

**Explanation:** Attackers often try random usernames. A high number of invalid users suggests dictionary/brute-force attacks.

---
