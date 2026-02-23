## HOW A ROUTER WORKS

### What is a Router?

A **router** is a network device that **connects different networks** and **forwards data packets** between them.

Think of a router as:

> A traffic police officer for network data
> 

---

### Why a Router is Needed

- Your home has a **local network (LAN)**
- The internet is a **different network**
- Router connects **LAN ↔ Internet (WAN)**

Without a router:

- Devices cannot access the internet
- Networks stay isolated

---

### How a Router Works (Step-by-Step)

Example: You open `google.com`

1️⃣ Your device creates a data packet

2️⃣ Packet is sent to the **router**

3️⃣ Router checks the **destination IP**

4️⃣ Router looks at its **routing table**

5️⃣ Router decides **where to send the packet next**

6️⃣ Packet is forwarded to ISP → Internet → Google server

When the reply comes back:

- Router sends it back to **your device**

---

### Important Router Functions

### 🔹 Routing

- Decides the **best path** for data
- Uses destination IP to forward packets

### 🔹 NAT (Network Address Translation)

- Converts **private IP → public IP**
- Allows multiple devices to share one internet connection

### 🔹 Firewall (Basic)

- Blocks or allows traffic based on rules
- Protects internal devices

---

### SOC Relevance

- Routers are **high-value targets**
- Router logs help detect:
    - Scanning
    - DDoS
    - Unauthorized access
- Misconfigured routers expose networks
