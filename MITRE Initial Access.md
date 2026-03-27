# INITIAL ACCESS (MITRE TACTIC)

---

## What is Initial Access?

### 🔹 Technical Definition

Initial Access is the tactic where an attacker first gains entry into a system or network.

It is the starting point of an attack.

Without Initial Access, no further attack stages can happen.

Think of it as:

> The entry point of the breach.
> 

---

## 🔹 Simple Explanation

If hacking is like breaking into a house,

Initial Access is:

> How the thief enters the house.
> 

If he never enters, he cannot steal anything.

---

## Why Initial Access is Important in SOC

Most SOC alerts begin at this stage.

If you detect early:

- Damage is small.
- Containment is easier.
- Business impact is reduced.

If you miss this stage:

- Attacker moves deeper.
- Harder to control.

---

# Common Initial Access Techniques

We focus only on SOC-relevant ones.

---

## 1️⃣ Brute Force

Attacker tries many passwords until one works.

### Logs Show:

- Multiple failed logins
- Possibly one successful login

### SOC Red Flags:

- Repeated 4625 (Windows)
- Repeated SSH failures (Linux)
- Same IP targeting same account

---

## 2️⃣ Phishing

Attacker sends malicious email.

User clicks link or opens attachment.

Malware executes.

### Logs Show:

- Suspicious email activity
- PowerShell execution
- Office macro activity
- Unexpected external connections

---

## 3️⃣ Exploiting Public-Facing Application

Attacker exploits vulnerability in web server.

Example:

- SQL injection
- Remote code execution

### Logs Show:

- Unusual HTTP requests
- Suspicious URL parameters
- Unexpected server-side processes

---

## 4️⃣ Valid Accounts

Attacker already has credentials.

Could be:

- Leaked password
- Credential stuffing
- Bought credentials

### Logs Show:

- Successful login
- No brute force pattern
- Login from unusual location

This one is dangerous because it looks normal.

---

# How Initial Access Appears in Investigation

You ask:

1️⃣ Was there authentication activity?

2️⃣ Was login successful?

3️⃣ From where?

4️⃣ Was it expected?

5️⃣ What happened after?

Initial Access is confirmed only when access succeeds.

Failed attempts alone = alert.

Successful unauthorized access = incident.

---

# Real Industry Example

Company detects:

- 50 failed login attempts from external IP
- Then successful login
- Then new admin created

Mapped as:

Initial Access via Brute Force → Persistence → Privilege Escalation

Investigation becomes structured.

---

# SOC Relevance

As L1, your job is:

- Identify Initial Access pattern
- Confirm if success occurred
- Check follow-up activity
- Escalate if compromise confirmed

You do NOT fix vulnerability.

You investigate and document.

---

# Common Beginner Mistakes

❌ Calling failed attempts an incident

❌ Ignoring what happens after login

❌ Not checking login type

❌ Not checking source IP reputation
