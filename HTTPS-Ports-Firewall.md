### HTTP (HyperText Transfer Protocol)

- Data is sent in **plain text**
- Anyone can read the data
- Not secure

Example:

- Passwords can be stolen easily

---

### 🔹 HTTPS (HTTP Secure)

- Uses **encryption (TLS)**
- Data is protected
- Secure communication

### Why HTTPS matters in security:

- Protects login credentials
- Prevents Man-in-the-Middle attacks
- Fake or invalid certificates can indicate attacks

##  PORTS

A **port** tells **which service** is running on a device.

Format:

```
IP :Port

```

Example:

```
192.168.1.10:443

```

### Common ports (MUST REMEMBER):

| Port | Service |
| --- | --- |
| 80 | HTTP |
| 443 | HTTPS |
| 21 | FTP |
| 22 | SSH |
| 23 | TELNET |
| 25 | SMTP |
| 3389 | RDP |
| 53 | DNS |
| 123 | NTP |

### Security importance:

- Open ports increase attack surface
- Port scanning = attacker recon
- Unknown open ports are suspicious

##  FIREWALL BASICS

A **firewall** controls network traffic by **allowing or blocking** connections based on rules.

Example rules:

- Allow port 443
- Block port 21

### Types:

- **Network firewall** – protects entire network
- **Host-based firewall** – protects single device

### Why firewalls are important:

- Prevent unauthorized access
- Firewall logs help detect attacks
- Multiple blocked attempts = attack attempt
