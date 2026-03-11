## 📂 Lesson 4: Logs (CORE SOC SKILL)

Read carefully. This lesson matters **more than tools, certs, or labs**.

---

## 1️⃣ What Are Logs (IN REAL TERMS)

**Logs are records of events**.

Every time something happens on a system:

- A user logs in
- A service starts
- A process fails
- A connection is made

➡️ It is written as a **log entry**.

SOC truth:

> **No logs = no visibility = blind security**
> 

---

## 2️⃣ Why Logs Are the HEART of SOC

SOC analysts don’t “hack”.

They **read logs and answer questions** like:

- Who logged in?
- From where?
- At what time?
- What failed?
- What changed?

Every alert you’ll ever see is based on **logs**.

---

## 3️⃣ Where Logs Live in Linux (VERY IMPORTANT)

Most logs are stored in:

```bash
/var/log
```

This directory is **SOC gold**.

---

## 4️⃣ Important Log Files You MUST Know

### 🔹 Authentication Logs

File:

```bash
/var/log/auth.log
```

Contains:

- Login attempts
- SSH access
- sudo usage

SOC relevance:

- Brute-force attacks
- Unauthorized access
- Privilege escalation

---

### 🔹 System Logs

File:

```bash
/var/log/syslog
```

Contains:

- System events
- Service messages
- Errors and warnings

SOC relevance:

- Malware activity
- Service abuse
- Unexpected behavior

---

### 🔹 Kernel Logs

File:

```bash
/var/log/kern.log
```

Contains:

- Kernel-level events
- Hardware and low-level messages

SOC relevance:

- Rootkits
- Low-level exploitation (advanced)

---

## 5️⃣ Reading Logs (COMMANDS YOU WILL USE DAILY)

### 🔹 Command 1: `ls`

👉 Run:

```bash
ls /var/log
```

Purpose:

- See what logs exist

---

### 🔹 Command 2: `cat`

👉 Run:

```bash
cat /var/log/syslog
```

Purpose:

- Display entire log file

⚠️ Logs can be very long. This is normal.

---

### 🔹 Command 3: `less` (VERY IMPORTANT)

👉 Run:

```bash
less /var/log/syslog
```

Controls inside `less`:

- `↑ ↓` → scroll
- `/keyword` → search
- `q` → quit

SOC relevance:

- This is how analysts actually read logs

---

### 🔹 Command 4: `tail`

👉 Run:

```bash
tail /var/log/syslog
```

Shows:

- Last 10 log entries

SOC relevance:

- Recent activity
- Incident timelines

---

### 🔹 Command 5: `tail -f` (REAL-TIME)

👉 Run:

```bash
tail -f /var/log/syslog
```

Shows:

- Live log updates

Press:

```bash
Ctrl + C
```

to stop.

SOC relevance:

- Live monitoring during incidents

---

## 6️⃣ What a Log Entry Looks Like (UNDERSTAND THIS)

Example:

```
Sep1010:15:32 ubuntu sshd[1234]: Failedpasswordfor invaliduseradminfrom192.168.1.5
```

Breakdown:

- **Date & time** → when
- **Host** → where
- **Service** → who generated log
- **Message** → what happened
- **IP** → source

SOC thinking:

> Failed login + unknown user + repeated attempts = 🚨
> 

---

## 7️⃣ Common SOC Red Flags in Logs

🚨 Look for:

- Multiple failed login attempts
- Repeated SSH failures
- sudo used unexpectedly
- Services restarting frequently
- Access from unknown IPs

These are **alert triggers**.

---

## 8️⃣ Logs Are Passive (IMPORTANT CONCEPT)

Logs:

- Do **not** stop attacks
- Do **not** block users
- Only **record events**

SOC work:

> Detect → Analyze → Respond
> 

---

# 📘 SUMMARY TABLE (ADD TO NOTES)

## 📂 LOG FILES

| File | Use | Example |
| --- | --- | --- |
| `/var/log` | Log directory | `/var/log` |
| `auth.log` | Authentication events | SSH logins |
| `syslog` | System events | Service messages |
| `kern.log` | Kernel events | Low-level activity |

---

## 💻 LOG COMMANDS

| Command | Use | Example |
| --- | --- | --- |
| `ls` | List log files | `ls /var/log` |
| `cat` | View entire log | `cat auth.log` |
| `less` | Scroll logs | `less syslog` |
| `tail` | Last entries | `tail syslog` |
| `tail -f` | Live logs | `tail -f syslog` |

---

## 🎤 INTERVIEW-READY LINES

Say these confidently:

- **“Logs provide visibility into system and user activity.”**
- **“SOC analysts investigate incidents by correlating log events.”**
- **“Authentication logs are crucial for detecting brute-force attacks.”**
- **“Logs are passive; they help detect but not prevent attacks.”**
