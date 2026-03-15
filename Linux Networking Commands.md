## Lesson 6: Linux Networking Commands (ss, ip)

This lesson connects:

**Networking basics + Linux + SOC detection**

This is where analysts detect **connections, listeners, and suspicious traffic**.

---

## 1️⃣ Why Linux Networking Commands Matter (SOC REALITY)

SOC analysts ask questions like:

- Which ports are open?
- Which process is listening?
- Who is connected right now?
- Is a service exposed unexpectedly?

Linux networking commands answer **exactly these**.

---

## 2️⃣ `ss` — SOCKET STATISTICS (MOST IMPORTANT)

`ss` replaces the old `netstat`.

This is what analysts actually use.

---

### 🔹 View listening ports

👉 Run:

```bash
ss -l
```

Meaning:

- `l` → listening sockets

SOC relevance:

- What services are waiting for connections

---

### 🔹 View TCP listening ports (IMPORTANT)

👉 Run:

```bash
ss -tuln
```

Breakdown:

- `t` → TCP
- `u` → UDP
- `l` → listening
- `n` → numeric (no DNS)

SOC relevance:

- Identify exposed services
- Detect unexpected listeners

---

### 🔹 Show process using the port (CRITICAL)

👉 Run:

```bash
ss -tulpn
```

SOC relevance:

- Which **process** owns which **port**
- Direct mapping: port → PID → process

---

## 3️⃣ `ip` — NETWORK CONFIGURATION TOOL

`ip` is the modern replacement for `ifconfig`.

---

### 🔹 Show IP address

👉 Run:

```bash
ip a
```

SOC relevance:

- Identify interfaces
- IP addresses during incidents

---

### 🔹 Show routing table

👉 Run:

```bash
ip route
```

SOC relevance:

- Where traffic is going
- Detect suspicious routes

---

## 4️⃣ Real SOC Scenarios (UNDERSTAND THIS)

### 🚨 Scenario 1: Unexpected open port

- Use:

```bash
ss -tulpn
```

- Ask:
    - Why is this port open?
    - Should this service be running?

---

### 🚨 Scenario 2: Suspicious outbound connection

- Combine with processes:

```bash
ps aux
ss -tup
```

SOC thinking:

- Malware needs network access
- Processes + connections = evidence

---

## 5️⃣ Difference Between `ss` and `nmap`

| Tool | Purpose |
| --- | --- |
| `ss` | What THIS system is doing |
| `nmap` | What OTHER systems expose |

SOC analysts use:

- `ss` internally
- SIEM externally
- nmap only in controlled situations

---

# 📘 SUMMARY TABLE (ADD TO NOTES)

## 🌐 NETWORKING COMMANDS

| Command | Use | Example |
| --- | --- | --- |
| `ss -l` | Listening sockets | `ss -l` |
| `ss -tuln` | TCP/UDP listeners | `ss -tuln` |
| `ss -tulpn` | Ports + process | `ss -tulpn` |
| `ip a` | Show IP addresses | `ip a` |
| `ip route` | Show routing table | `ip route` |

---

## 🎤 INTERVIEW-READY LINES

You can safely say:

- **“`ss` is used to identify listening ports and active connections on a Linux system.”**
- **“Mapping ports to processes helps detect unauthorized services.”**
- **“`ip a` and `ip route` are used to inspect network interfaces and routing paths.”**
- **“Unexpected listening ports are a common SOC investigation trigger.”**
