# 🔹 ICMP (Internet Control Message Protocol)

## What is ICMP?

**ICMP** is a protocol used to **send error messages and status information** between network devices.

👉 ICMP is **not used to transfer data** like TCP/UDP.

It is used to **report problems** in the network.

Think of ICMP as:

> Network’s feedback & error reporting system
> 

---

## Common ICMP Uses

### 1️⃣ Ping

- Uses ICMP to check if a device is reachable
- Sends an **Echo Request**
- Receives an **Echo Reply**

Example:

```bash
ping google.com

```

---

### 2️⃣ Error Reporting

ICMP tells:

- Destination unreachable
- Request timed out
- Network unreachable

---

## Important ICMP Messages (You should know)

| ICMP Message | Meaning |
| --- | --- |
| Echo Request | Ping request |
| Echo Reply | Ping response |
| Destination Unreachable | Target cannot be reached |
| Time Exceeded | Packet took too long |

---

## Security & SOC Relevance

### Why ICMP is important:

- Used in **network troubleshooting**
- Helps detect connectivity issues

### Security risks:

- ICMP Flood → **DDoS attack**
- Ping scans used for **reconnaissance**
- Attackers map live hosts using ICMP

### SOC handling:

- Excessive ICMP traffic = suspicious
- ICMP often restricted by firewalls
- ICMP logs help identify scanning activity

---

## Important Point to Remember

- ICMP **does NOT use ports**
- ICMP works directly over IP

# 🔹 NTP (Network Time Protocol)

## What is NTP?

**NTP** is a protocol used to **synchronize time** between computers.

👉 All systems in a network must have **accurate time**.

Think of NTP as:

> Clock synchronization service for computers
> 

---

## Port Number

```
NTP → UDP Port123

```

---

## Why NTP is VERY IMPORTANT in Cybersecurity

### 1️⃣ Log Correlation

- SOC analysts rely on timestamps
- Incorrect time = logs don’t match
- Incident investigation becomes impossible

---

### 2️⃣ Incident Response

- Accurate time helps:
    - Track attack timeline
    - Identify first compromise
    - Correlate events across systems

---

## Security Risks of NTP

### 1️⃣ NTP Amplification Attack

- Used in **DDoS attacks**
- Small request → very large response
- Attacker spoofs victim IP

---

### 2️⃣ Time Manipulation

- If attacker controls NTP:
    - Logs become unreliable
    - Attacks are harder to trace

---

## SOC Relevance

- NTP traffic should be monitored
- Unauthorized NTP servers = red flag
- Time drift issues indicate misconfiguration or attack

---

## Important Points to Remember

- NTP uses **UDP**
- NTP uses **port 123**
- Time sync is **critical for SOC work**

# 🔹 DDoS (Distributed Denial of Service)

## What is DDoS?

A **DDoS attack** is an attack where **multiple systems (computers/bots)** send a huge amount of traffic to a target server **at the same time**, causing it to **slow down or completely stop working**.

Think of DDoS as:

> 1000 people calling one phone number at once so real calls can’t get through
> 

---

## Why it is called *Distributed*

- The attack comes from **many sources**, not one
- These sources are usually:
    - Infected computers (botnet)
    - Servers
    - IoT devices

Explain in interview:

> “DDoS is dangerous because traffic comes from many IPs, making blocking difficult.”
> 

---

## Goal of a DDoS Attack

- Make a website or service **unavailable**
- Exhaust:
    - Bandwidth
    - Server resources
    - Network capacity

❗ Data theft is **NOT** the goal — **disruption is**

---

## Common Types of DDoS Attacks (SOC-Level)

### 1️⃣ Volume-Based Attacks

- Flood the target with massive traffic
- Example:
    - ICMP flood
    - UDP flood

📌 Effect:

- Network bandwidth gets exhausted

---

### 2️⃣ Protocol Attacks

- Exploit weaknesses in network protocols
- Example:
    - SYN flood

📌 Effect:

- Server resources are exhausted

---

### 3️⃣ Application Layer Attacks

- Target web applications
- Example:
    - HTTP flood

📌 Effect:

- Website becomes slow or crashes

---

## DDoS vs DoS (Important Difference)

| DoS | DDoS |
| --- | --- |
| Single attacker | Multiple attackers |
| Easier to block | Harder to block |
| Limited impact | Large-scale impact |

---

## Signs of a DDoS Attack (SOC View)

- Sudden traffic spike
- Website becomes slow or unavailable
- Many requests from multiple IPs
- Repeated requests to same endpoint

---

## How SOC Teams Detect DDoS

- Network traffic monitoring
- Firewall & IDS alerts
- Abnormal bandwidth usage
- Logs showing repeated requests

---

## How DDoS is Mitigated (High Level)

- Rate limiting
- Traffic filtering
- Blocking malicious IPs
- Using DDoS protection services

(No deep implementation required at entry level)

---

## Important Points to Remember

- DDoS = **Availability attack**
- Affects **CIA Triad → Availability**
- Often uses **UDP, ICMP, HTTP**
- Uses **botnets**
- Hard to block due to distributed nature

---

## ✅ QUICK MEMORY SUMMARY

- **DDoS = many systems flooding one target**
- **Goal = service down, not data theft**
- **SOC role = detect, alert, mitigate**
