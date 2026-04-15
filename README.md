
#  Task 4: Setup and Use a Firewall on Linux (UFW)

> **Cybersecurity Internship** | Firewall Configuration & Network Traffic Filtering  
> **Platform:** Kali Linux | **Tool:** UFW (Uncomplicated Firewall)

---

## 📌 Objective

Configure and test basic firewall rules using UFW on Kali Linux to allow or block network traffic on specific ports.

---

## 🛠️ Tools Used

| Tool | Purpose |
|------|---------|
| UFW (Uncomplicated Firewall) | Firewall configuration on Linux |
| Telnet | Testing port 23 connectivity |
| Netcat (`nc`) | Verifying port block |
| Kali Linux Terminal | Command execution |

---

## ✅ Steps Performed

### Step 1 — Open Firewall Configuration Tool
Opened the terminal on Kali Linux and used UFW as the firewall management tool.

```bash
sudo apt install ufw -y
sudo ufw enable
```

---

### Step 2 — List Current Firewall Rules
Checked the existing firewall rules to understand the baseline configuration.

```bash
sudo ufw status numbered verbose
```

**Output:** UFW status showed as `active` with no rules initially.

---

### Step 3 — Block Inbound Traffic on Port 23 (Telnet)
Added a rule to deny all incoming Telnet traffic on port 23.

```bash
sudo ufw deny in 23/tcp
sudo ufw status numbered
```

**Result:**
```
[ 1] 23/tcp    DENY IN    Anywhere
[ 2] 23/tcp (v6)  DENY IN    Anywhere (v6)
```

---

### Step 4 — Test the Block Rule
Attempted to connect to localhost on port 23 using both `telnet` and `netcat` to verify the rule was working.

```bash
telnet 127.0.0.1 23
nc -zv 127.0.0.1 23
```

**Output:**
```
telnet: Unable to connect to remote host: Connection refused
localhost [127.0.0.1] 23 (telnet) : Connection refused
```
✅ Block rule confirmed working.

---

### Step 5 — Allow SSH (Port 22)
Added a rule to allow inbound SSH traffic for secure remote access.

```bash
# Allow SSH inbound
sudo ufw allow 22/tcp

# Verify
sudo ufw status numbered
```

**Result:**
```
[ 1] 23/tcp      DENY IN    Anywhere
[ 2] 22/tcp      ALLOW IN   Anywhere
[ 3] 23/tcp (v6) DENY IN    Anywhere (v6)
[ 4] 22/tcp (v6) ALLOW IN   Anywhere (v6)
```

---

### Step 6 — Remove the Test Block Rule
Deleted the deny rule for port 23 to restore the original firewall state.

```bash
sudo ufw status numbered
sudo ufw delete 1
sudo ufw status numbered
```

**Output after deletion:**
```
Deleting: deny 23/tcp
Proceed with operation (y|n)? y
Rule deleted

[ 1] 22/tcp      ALLOW IN   Anywhere
[ 2] 23/tcp (v6) DENY IN    Anywhere (v6)
[ 3] 22/tcp (v6) ALLOW IN   Anywhere (v6)
```

---

### Step 7 — Command Reference

| Action | Command |
|--------|---------|
| Install UFW | `sudo apt install ufw -y` |
| Enable firewall | `sudo ufw enable` |
| Disable firewall | `sudo ufw disable` |
| View rules (numbered) | `sudo ufw status numbered` |
| Block port 23 (TCP) | `sudo ufw deny in 23/tcp` |
| Allow port 22 (SSH) | `sudo ufw allow 22/tcp` |
| Delete rule by number | `sudo ufw delete <number>` |
| Set default deny inbound | `sudo ufw default deny incoming` |
| Reset all rules | `sudo ufw reset` |

---

### Step 8 — How a Firewall Filters Traffic

A firewall inspects incoming and outgoing network packets and compares them against a defined **ruleset**. Each rule specifies:
- **Port** — e.g., 22, 23, 80, 443
- **Protocol** — TCP or UDP
- **Direction** — Inbound (IN) or Outbound (OUT)
- **Action** — ALLOW or DENY

**UFW Rule Processing:**
- Rules are processed **top to bottom** — first match wins
- Blocking port **23 (Telnet)** prevents unencrypted remote login attempts
- Allowing port **22 (SSH)** permits secure encrypted remote administration
- Best practice: `sudo ufw default deny incoming` — deny everything unless explicitly allowed

---

## 📸 Screenshots

| Screenshot | Description |
|-----------|-------------|
| `screenshot1.png` | UFW status after blocking port 23 + Telnet/Netcat connection refused |
| `screenshot2.png` | UFW rules showing port 22 allowed and port 23 blocked |
| `screenshot3.png` | Deleting the block rule and final restored state |
![Alt text](https://github.com/mynamevarkey/-Task-4-Setup-and-Use-a-Firewall-on-Linux-UFW-/blob/main/Screenshot%20From%202026-04-15%2014-44-33.png)
![Alt text](https://github.com/mynamevarkey/-Task-4-Setup-and-Use-a-Firewall-on-Linux-UFW-/blob/main/Screenshot%20From%202026-04-15%2014-44-15.png)
![Alt text](https://github.com/mynamevarkey/-Task-4-Setup-and-Use-a-Firewall-on-Linux-UFW-/blob/main/Screenshot%20From%202026-04-15%2014-44-43.png)


---

## 📊 Outcome

Successfully demonstrated:
- ✅ Basic firewall management using UFW on Kali Linux
- ✅ Blocking insecure protocols (Telnet - port 23)
- ✅ Allowing secure access (SSH - port 22)
- ✅ Testing and verifying firewall rules
- ✅ Restoring firewall to original state
- ✅ Understanding of network traffic filtering principles

---


---

## 📁 Repository Structure

```
firewall-task/
├── README.md               ← This file
├── screenshots/
│   ├── screenshot1.png     ← Block rule + connection refused
│   ├── screenshot2.png     ← All rules listed (port 22 + 23)
│   └── screenshot3.png     ← Rule deleted, state restored
```

---

*Completed as part of Cybersecurity Internship — Task 4: Firewall Configuration*
