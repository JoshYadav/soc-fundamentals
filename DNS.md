## DNS (Domain Name System)

DNS converts **domain names into IP addresses**.

Example:

```
google.com → 142.250.xxx.xxx

```

Think of DNS as:

> Internet phonebook
> 

### How DNS works:

1. You type a website name
2. DNS finds its IP address
3. Browser connects to that IP

### Why DNS is Needed

- Computers understand IP addresses
- Humans remember names
- DNS bridges the gap

---

### How DNS Works (FULL FLOW)

Example: You type `google.com`

1️⃣ Browser checks **local cache**

2️⃣ If not found, request goes to **DNS Resolver**

3️⃣ Resolver contacts **Root DNS Server**

4️⃣ Root server points to **TLD server (.com)**

5️⃣ TLD server points to **Authoritative DNS server**

6️⃣ Authoritative server returns **IP address**

7️⃣ Browser connects to the IP

Now the website loads.

---

### Types of DNS Servers

| Server Type | Role |
| --- | --- |
| Resolver | First contact |
| Root | Directs to TLD |
| TLD | Directs to authoritative |
| Authoritative | Gives final IP |

---

### Common DNS Records (SOC-Level)

| Record | Purpose |
| --- | --- |
| A | Domain → IPv4 |
| AAAA | Domain → IPv6 |
| CNAME | Alias |
| MX | Mail servers |
| TXT | Verification |

### Why DNS is important in SOC:

- Malware communicates using DNS
- Fake websites use look-alike domains
- Random domain names are red flags
- Phishing relies on fake domains
- DNS tunneling hides data
