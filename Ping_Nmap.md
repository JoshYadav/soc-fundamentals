# `ping`

## What is `ping`?

`ping` is a command used to **check whether a device is reachable over a network**.

It works using **ICMP**.

Think of `ping` as:

> “Are you alive? Please reply.”
> 

---

## How `ping` works

1. Your system sends an **ICMP Echo Request**
2. Target system replies with **ICMP Echo Reply**
3. Time taken is measured (latency)

Example:

```bash
ping google.com

```

---

## What `ping` tells you

- Whether the target is **reachable**
- **Response time** (latency)
- Packet loss (if any)

---

## SOC / Security relevance

- Used to check if a server is **up or down**
- Used by attackers for **reconnaissance**
- Excessive ping = possible **ICMP flood**

---

## Important points

- `ping` does **NOT use ports**
- Uses **ICMP**
- Many servers block ping for security

---

# 🔹 `tracert` / `traceroute`

## What is `tracert / traceroute`?

This command shows the **path taken by packets** from your system to a destination.

- Windows → `tracert`
- Linux / macOS → `traceroute`

Think of it as:

> “Show me all the stops between me and the destination.”
> 

---

## How it works (simple)

- Sends packets with increasing **TTL (Time To Live)**
- Each router reduces TTL by 1
- When TTL = 0, router replies
- This reveals each hop (router)

Example:

```bash
tracert google.com

```

---

## What it shows

- Each router (hop) between source and destination
- Time taken to reach each hop
- Where packets are slowing or failing

---

## SOC / Security relevance

- Helps identify **network bottlenecks**
- Helps trace where traffic is blocked
- Used in **attack path analysis**
- Attackers may use it for **network mapping**

---

## Important points

- Uses **ICMP** (mostly)
- Can be blocked by firewalls
- Timeouts don’t always mean failure

---

# 🔹 `nmap`

## What is `nmap`?

`nmap` is a **network scanning tool** used to discover:

- Live hosts
- Open ports
- Services running on systems

Think of `nmap` as:

> “Knocking on doors to see which ones are open.”
> 

---

## What `nmap` does

- Scans IP addresses
- Identifies **open ports**
- Detects running services

Example:

```bash
nmap 192.168.1.10

```

---

## SOC / Security relevance

- Used by attackers for **reconnaissance**
- Used by defenders to:
    - Find open ports
    - Identify attack surface
- `nmap` activity in logs = **possible attack**

---

## Important points

- `nmap` usually uses **TCP**
- Scans can be noisy
- Should be monitored in SOC environments

---

| Command | Purpose |
| --- | --- |
| `ifconfig` | Get IP address |
| `hostname -I` | Alternate IP method |
| `nmap --version` | Check installation |
| `nmap 127.0.0.1` | Scan own device |
| `nmap <IP>` | Scan single host |
| `nmap 192.168.1.1` | Scan router |
| `nmap -sn 192.168.1.0/24` | Host discovery |
| `nmap -sn 192.168.1.0/24 -v` | Verbose discovery |
| `nmap 192.168.1.0/24 -v` | ❌ Noisy scan |

# 🔹 `nslookup`

## What is `nslookup`?

`nslookup` is a command used to **query DNS servers** and find IP addresses for domain names.

Think of `nslookup` as:

> “Ask DNS: what is the IP of this domain?”
> 

---

## How it works

- Sends a DNS query
- Receives IP address or DNS records

Example:

```bash
nslookup google.com

```

---

## What `nslookup` shows

- Domain → IP address
- Which DNS server responded
- DNS resolution issues

---

## SOC / Security relevance

- Used to investigate **suspicious domains**
- Helps identify phishing or malware domains
- DNS anomalies are common attack indicators

---

## Important points

- Uses **DNS (UDP port 53)**
- Useful for DNS troubleshooting
- Often used during incident investigation

---

## ✅ QUICK MEMORY SUMMARY

- **ping** → checks reachability (ICMP)
- **tracert / traceroute** → shows network path
- **nmap** → scans ports & services
- **nslookup** → queries DNS information
