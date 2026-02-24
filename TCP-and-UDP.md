### 🔹 TCP (Transmission Control Protocol)

TCP is a **reliable communication method**.

Characteristics:

- Connection-oriented
- Data is sent in order
- Receiver confirms data is received

Used in:

- Websites
- Login systems
- Emails
- File transfers

📌 Example:

If you log into Gmail, TCP ensures your password reaches correctly.

### Security importance:

- Easier to track sessions
- Most authentication attacks use TCP

### 🔹 TCP/IP MODEL

The **TCP/IP model** explains **how data moves from one device to another** over a network.

It has **4 layers** (remember this order).

---

### 🔹 1. Application Layer

This is where **user-level communication** happens.

Examples:

- HTTP / HTTPS
- FTP
- SMTP
- DNS
- SSH

📌 What it does:

- Prepares data for transmission
- Handles services like web browsing and email

SOC relevance:

- Most attacks target this layer (web attacks, phishing)

---

### 🔹 2. Transport Layer

Responsible for **end-to-end communication**.

Protocols:

- **TCP**
- **UDP**

📌 What it does:

- Breaks data into segments
- Ensures delivery (TCP)
- Uses ports

SOC relevance:

- Port scanning, brute force, DDoS happen here

---

### 🔹 3. Internet Layer

Responsible for **logical addressing and routing**.

Protocols:

- IP (IPv4, IPv6)
- ICMP

📌 What it does:

- Decides where data should go
- Handles IP addresses

SOC relevance:

- IP-based attacks, spoofing, scanning

---

### 🔹 4. Network Access Layer

Handles **physical transmission** of data.

Includes:

- Ethernet
- Wi-Fi
- MAC addresses

📌 What it does:

- Sends data as bits over hardware

SOC relevance:

- MAC-based filtering, local attacks

---

### 🔑 Easy Memory Trick

**A → T → I → N**

**Application → Transport → Internet → Network**

### 🔹 OSI MODEL vs TCP/IP MODEL

Both models explain **how data travels across a network**, but with different complexity.

---

### OSI MODEL (7 Layers)

OSI is a **conceptual model** used for **learning and troubleshooting**.

| Layer | Purpose |
| --- | --- |
| 7 Application | User interaction |
| 6 Presentation | Encryption |
| 5 Session | Session control |
| 4 Transport | TCP/UDP |
| 3 Network | IP routing |
| 2 Data Link | MAC |
| 1 Physical | Hardware |

---

## TCP/IP MODEL (4 Layers)

TCP/IP is a **practical model** used in **real networks**.

| Layer | Purpose |
| --- | --- |
| Application | User services |
| Transport | TCP/UDP |
| Internet | IP |
| Network Access | Hardware |

---

## OSI vs TCP/IP (DIRECT COMPARISON)

| Feature | OSI | TCP/IP |
| --- | --- | --- |
| Layers | 7 | 4 |
| Usage | Theoretical | Practical |
| Complexity | High | Simple |
| Real-world use | Rare | Actual internet |

---

### Layer Mapping (IMPORTANT)

| OSI | TCP/IP |
| --- | --- |
| Application + Presentation + Session | Application |
| Transport | Transport |
| Network | Internet |
| Data Link + Physical | Network Access |

---

### SOC Relevance

- OSI helps **pinpoint attack layer**
- TCP/IP reflects **real traffic**
- Logs follow TCP/IP structure

### 🔹 TCP FLAGS

TCP flags are **control bits** used to **manage connections**.

Each flag has a **specific meaning**.

---

### 🔹 Common TCP Flags (IMPORTANT)

| Flag | Meaning | Purpose |
| --- | --- | --- |
| SYN | Synchronize | Start connection |
| ACK | Acknowledgement | Confirm data |
| FIN | Finish | Close connection |
| RST | Reset | Force close |
| PSH | Push | Send data immediately |
| URG | Urgent | Priority data |

---

### SOC relevance of flags

- **SYN floods** → DDoS attack
- **RST** → connection reset
- Abnormal flag combinations → suspicious traffic

### 🔹 TCP THREE-WAY HANDSHAKE

This is the process TCP uses to **establish a connection**.

It happens **before any data is sent**.

### 🔹 Step-by-step Handshake

### 1️⃣ SYN

Client → Server

> “Can we start a connection?”
> 

### 2️⃣ SYN-ACK

Server → Client

> “Yes, I’m ready.”
> 

### 3️⃣ ACK

Client → Server

> “Confirmed. Let’s communicate.”
> 

After this → **connection is established**.

### Why this is important

- Ensures both devices are ready
- Prevents data loss
- Creates a session

SOC relevance:

- **SYN flood attacks** exploit this process
- Handshake failures indicate network issues or attacks

### Easy Memory Trick

**SYN → SYN-ACK → ACK**

Think: **Request → Accept → Confirm**

## 🔹UDP(User Datagram Protocol)

UDP is a **fast but unreliable communication method**.

Characteristics:

- Connectionless
- No confirmation of delivery
- Faster than TCP

Used in:

- DNS
- Video streaming
- Online games

### Security importance:

- Commonly used in **DDoS attacks**
- Harder to track because no sessions


## TCP vs UDP (TABLE)

| Feature | **TCP** | **UDP** |
| --- | --- | --- |
| Full form | Transmission Control Protocol | User Datagram Protocol |
| Connection type | Connection-oriented | Connectionless |
| Reliability | Reliable (guaranteed delivery) | Unreliable (no guarantee) |
| Data order | Maintains correct order | Order not guaranteed |
| Acknowledgement | Yes (ACKs used) | No acknowledgements |
| Speed | Slower than UDP | Faster than TCP |
| Packet loss handling | Retransmits lost packets | Does not retransmit |
| Session tracking | Yes (sessions exist) | No sessions |
| Common usage | Web browsing, login, email | DNS, streaming, gaming |
| Security relevance | Used in authentication & login attacks | Used in DDoS & flooding attacks |
| Example | HTTPS (port 443) | DNS (port 53) |
