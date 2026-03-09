## 🔐 Lesson 2: Users, Groups & File Permissions (CRITICAL)

This lesson is **security-core**, not “Linux basics”.

Most real incidents happen because of **permission mistakes**.

Read carefully.

---

## 1️⃣ Why Users & Permissions Exist (SECURITY LOGIC)

Linux follows **least privilege**:

> A user should have **only the access they need**, nothing more.
> 

Why?

- Prevent accidental damage
- Limit attacker movement
- Contain breaches

SOC relevance:

- Most compromises start with a **low-privileged user**
- Attackers try to **escalate privileges**

---

## 2️⃣ Linux User Types (IMPORTANT)

### 🔹 Root user

- Superuser
- Full control over system
- UID = `0`

⚠️ SOC note:

- If an attacker becomes root → **game over**

---

### 🔹 Normal users

- Daily users (like you: `josh`)
- Limited permissions
- Cannot change system files

SOC relevance:

- Attacks usually start here

---

### 🔹 System users

- Created for services (web server, database, etc.)
- No login shell

SOC relevance:

- Compromised services = stealthy attacks

---

## 3️⃣ Groups (ACCESS CONTROL)

Groups allow:

- Multiple users
- Shared permissions
- Easier management

Example:

- `sudo` group → admin privileges

SOC relevance:

- Attackers try to add themselves to **privileged groups**

---

## 4️⃣ File Permissions (MOST IMPORTANT PART)

Run:

```bash
ls -l
```

You’ll see something like:

```
-rwxr-xr--
```

Break it down:

| Section | Meaning |
| --- | --- |
| `-` | File type |
| `rwx` | Owner permissions |
| `r-x` | Group permissions |
| `r--` | Others permissions |

---

## 5️⃣ Permission Types (MEMORIZE MEANING)

| Permission | Meaning |
| --- | --- |
| `r` | Read |
| `w` | Write |
| `x` | Execute |

SOC relevance:

- `x` on scripts = execution
- `w` on configs = persistence
- Misplaced `r` = data leakage

---

## 6️⃣ Numeric Permissions (YOU MUST KNOW)

| Number | Permission |
| --- | --- |
| 4 | Read |
| 2 | Write |
| 1 | Execute |

Examples:

- `7` → rwx
- `6` → rw-
- `5` → r-x

Example:

```bash
chmod 755 file.sh
```

SOC relevance:

- World-writable files (`777`) = 🚨 red flag

---

## 7️⃣ Ownership (WHO OWNS THE FILE)

Every file has:

- Owner
- Group

Command:

```bash
ls -l
```

Change owner:

```bash
chown user:group file
```

SOC relevance:

- Malware often **changes ownership**
- Attackers hide under legitimate users

---

## 8️⃣ sudo (CONTROLLED POWER)

`sudo` = temporary admin access

Example:

```bash
sudo apt update
```

SOC relevance:

- Logs show sudo usage
- Unexpected sudo = investigation trigger

---

## ⚠️ REAL SOC SCENARIOS (READ THIS)

🚨 Red flags you’ll investigate in future:

- Files with `777` permissions
- Scripts executable by everyone
- Users added to `sudo`
- Modified `/etc` files
- Suspicious ownership changes

This lesson connects **directly** to:

- Privilege escalation
- Incident response
- Forensics

## 👤 USERS & GROUPS

| Item | Use | Example |
| --- | --- | --- |
| Root user | Full system control | `sudo su` |
| Normal user | Daily operations | `josh` |
| Group | Shared permissions | `sudo` |
| `whoami` | Show current user | `whoami` |
| `groups` | Show user groups | `groups` |

---

## 🔐 PERMISSIONS & OWNERSHIP

| Command | Use | Example |
| --- | --- | --- |
| `ls -l` | View permissions | `ls -l` |
| `chmod` | Change permissions | `chmod 755 file.sh` |
| `chown` | Change ownership | `chown user:group file` |
| `sudo` | Admin privilege | `sudo apt update` |

---

## 🎤 INTERVIEW-READY ONE-LINERS

You can safely say these:

- **“Linux enforces least privilege using users, groups, and permissions.”**
- **“Most attacks start with low privileges and attempt escalation.”**
- **“World-writable files are a common security misconfiguration.”**
- **“Unexpected sudo usage is a key SOC investigation indicator.”**
