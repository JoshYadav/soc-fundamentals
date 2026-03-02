# IDS (INTRUSION DETECTION SYSTEM)

## What is IDS?

An **IDS** is a security system that **monitors network or system activity** and **detects suspicious behavior**.

👉 IDS **detects but does NOT block** attacks.

Think of IDS as:

> Security camera that raises an alarm
> 

---

## Types of IDS

### 1️⃣ Network-based IDS (NIDS)

- Monitors **network traffic**
- Placed at strategic points in the network

Detects:

- Port scanning
- DDoS attempts
- Suspicious traffic patterns

---

### 2️⃣ Host-based IDS (HIDS)

- Installed on a **single system**
- Monitors:
    - File changes
    - System logs
    - User activity

Detects:

- Unauthorized file access
- Privilege escalation attempts

---

## How IDS Detects Attacks

### 1️⃣ Signature-based detection

- Matches traffic against **known attack patterns**
- Example: known malware signature

✅ Accurate for known attacks

❌ Cannot detect new (zero-day) attacks

---

### 2️⃣ Anomaly-based detection

- Learns **normal behavior**
- Flags anything abnormal

✅ Can detect unknown attacks

❌ Can generate false alerts

---

## IDS Alerts & SOC Role

When IDS detects something:

1. Alert is generated
2. SOC analyst investigates
3. Decide:
    - False positive
    - Real attack
4. Escalate if needed

---

## IDS Limitations (IMPORTANT)

- Cannot block attacks
- Can generate false positives
- Needs human analysis

### 🔹 IPS (Intrusion Prevention System)

- Monitors traffic
- Detects threats
- **Automatically blocks attacks**

Think of IPS as:

> Security guard
> 

### SOC relevance:

- IDS alerts require investigation
- IPS blocks trigger incident response
- False alerts must be handled carefully

## IDS vs IPS (Quick Reminder)

| Feature | IDS | IPS |
| --- | --- | --- |
| Detect | ✅ Yes | ✅ Yes |
| Block | ❌ No | ✅ Yes |
| Alerts | ✅ Yes | ✅ Yes |
| Action | Manual (SOC analyst) | Automatic |

## SOC INTERVIEW GOLD POINTS

- IDS is **detective control**
- IPS is **preventive control**
- IDS alerts require human investigation
- IDS logs are key input for SIEM
