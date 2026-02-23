## 1️⃣ IP ADDRESS & MAC ADDRESS

### 🔹 IP Address (Internet Protocol Address)

An **IP address** is a number given to a device so it can **send and receive data on a network**.

Example:

```
192.168.1.10

```

Think of IP as:

> Home address of a device
> 

### Types of IP:

- **Private IP**
    - Used inside local networks (WiFi, office, college)
    - Example: `192.168.x.x`
    - Not visible on the internet
- **Public IP**
    - Given by ISP
    - Used to communicate over the internet
    - Visible to websites and attackers

### Why IP is important in cybersecurity:

- Every log contains **source IP** and **destination IP**
- Attacks are identified using suspicious IPs
- Repeated requests from same IP = possible attack

## 🔹IPv4 vs IPv6

IP addresses identify **devices on a network**.

---

### 🔹 IPv4

Example:

```
192.168.1.1

```

Characteristics:

- 32-bit address
- About 4.3 billion addresses
- Widely used today

Limitations:

- Address exhaustion
- Needs NAT

SOC relevance:

- Most logs still use IPv4
- Common target for attacks

---

### 🔹 IPv6

Example:

```
2001:0db8:85a3:0000:0000:8a2e:0370:7334

```

Characteristics:

- 128-bit address
- Huge address space
- No need for NAT

Advantages:

- Better security design
- Efficient routing

SOC relevance:

- Often **ignored in monitoring**
- Attackers exploit IPv6 blind spots

---

### 🔍 IPv4 vs IPv6 (TABLE)

| Feature | IPv4 | IPv6 |
| --- | --- | --- |
| Address size | 32-bit | 128-bit |
| Format | Numeric | Hexadecimal |
| Address space | Limited | Extremely large |
| NAT required | Yes | No |
| Adoption | Very common | Increasing |

### 🔹 MAC Address (Media Access Control)

A **MAC address** is a **hardware address** given to a network device.

Example:

```
00:1A:2B:3C:4D:5E

```

Think of MAC as:

> Permanent ID card of the device
> 

### Key points:

- Works only inside a **local network**
- Used before IP communication starts

### Why MAC matters in security:

- Used to identify devices inside a network
- Helpful in insider attacks and device tracking
