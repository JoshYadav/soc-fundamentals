## Lesson 1: Windows Architecture & Investigation Mindset

This phase is **non-negotiable** for SOC / Blue Team.

> **Reality:**
> 
> 
> 70–80% of SOC alerts come from **Windows endpoints**.
> 

You are not learning Windows like an admin.

You are learning Windows like an **investigator**.

---

## 1️⃣ How Windows Is Structured (ONLY WHAT YOU NEED)

Think of Windows as **4 investigation layers**:

### 🔹 Layer 1: User Layer

- Who logged in?
- From where?
- When?
- Using what account?

### 🔹 Layer 2: Process Layer

- What program ran?
- Who launched it?
- What did it spawn?

### 🔹 Layer 3: File Layer

- What files were created/modified/deleted?
- Where?
- By which process?

### 🔹 Layer 4: Registry & Persistence

- What survives reboot?
- Startup locations
- Scheduled tasks
- Registry Run keys

SOC investigations move **top → bottom**.

---

## 2️⃣ Windows vs Linux (SOC POV)

| Topic | Linux | Windows |
| --- | --- | --- |
| User auth | auth.log | Security Event Log |
| Processes | ps / top | Task Manager / Event Logs |
| Services | systemctl | Services.msc |
| Logs | /var/log | Event Viewer |
| Persistence | cron | Registry / Tasks |

You already know Linux side.

Now you mirror the same logic in Windows.

---

## 3️⃣ MOST IMPORTANT WINDOWS TOOL: Event Viewer

### What is Event Viewer?

> Central place where **Windows records everything important**.
> 

SOC analysts live here.

---

### How to open it:

- Press **Win + R**
- Type:

```
eventvwr.msc
```

- Press Enter

---

## 4️⃣ Event Viewer Structure (VERY IMPORTANT)

You will see:

### 📁 Windows Logs

These are the **core SOC logs**:

| Log | What it records | Importance |
| --- | --- | --- |
| Application | App errors | ⭐ |
| Security | Logins, processes | ⭐⭐⭐ |
| System | OS & services | ⭐⭐ |

👉 **Security log = MOST IMPORTANT**

---

## 5️⃣ Key SOC Concept: Event ID

Every Windows action has an **Event ID**.

Think of Event ID like:

> “grep keyword for Windows”
> 

Example:

- Linux: `grep "Failed password"`
- Windows: Event ID **4625**

You will memorize only **few critical IDs**, not hundreds.

---

## 6️⃣ FIRST EVENT IDS YOU MUST KNOW (NO MORE)

| Event ID | Meaning | SOC Use |
| --- | --- | --- |
| 4624 | Successful login | Who logged in |
| 4625 | Failed login | Brute force |
| 4634 | Logoff | Session end |
| 4688 | Process creation | Malware execution |
| 4720 | User created | Backdoor account |

That’s enough for now.

---

## 7️⃣ Investigation Mindset (THIS IS KEY)

When you see an alert, you ALWAYS ask:

1. **WHO** (user, account)
2. **WHAT** (process, action)
3. **WHERE** (host, IP)
4. **WHEN** (timestamp)
5. **HOW** (method)
6. **SO WHAT** (false positive or threat)

This mindset > tools.

---

## 8️⃣ What We Are NOT Doing Yet

❌ Active Directory

❌ Group Policy

❌ PowerShell scripting

❌ SIEM ingestion

❌ Sysmon

All later. Stored.

---

# 📘 SUMMARY TABLE (ADD TO NOTES)

| Item | Purpose |
| --- | --- |
| Event Viewer | Central Windows logs |
| Security Log | Authentication & processes |
| Event ID | Type of activity |
| 4624 | Successful login |
| 4625 | Failed login |
| 4688 | Process creation |

---

## 🔴 PRACTICAL TASK (MANDATORY)

On your **Windows VM**:

1️⃣ Open Event Viewer

2️⃣ Go to:

```
Windows Logs → Security
```

3️⃣ Scroll and:

- Find **Event ID 4624**
- Find **Event ID 4625**

Do NOT analyze deeply yet. Just observe.

## 🧠 Lesson 2: Users, Accounts & Logon Types (VERY IMPORTANT)

This lesson is **core SOC knowledge**.

Most real alerts = **login-related alerts**.

---

## 1️⃣ Windows Accounts You MUST Understand

Windows has **different account types**. SOC analysts must distinguish them.

### 🔹 Local User

- Created on a single machine
- Common in malware persistence

### 🔹 Administrator

- High privilege
- Abuse = **CRITICAL ALERT**

### 🔹 System / Service Accounts

- `SYSTEM`
- `LOCAL SERVICE`
- `NETWORK SERVICE`

👉 These **should not log in interactively**.

If they do = 🚨

---

## 2️⃣ Where to View Users

### Method 1 (GUI):

- Press **Win + R**
- Type:

```
lusrmgr.msc
```

- Go to:
    - Users
    - Groups

SOC use:

- Detect newly created users
- Detect admin group abuse

---

### Method 2 (Command line):

Open **Command Prompt**:

```bash
net user
```

Shows all users.

Check a specific user:

```bash
net user username
```

---

## 3️⃣ Event IDs for User Activity (LOCK THESE)

| Event ID | Meaning | Severity |
| --- | --- | --- |
| 4624 | Successful logon | Medium |
| 4625 | Failed logon | Medium |
| 4720 | User created | High |
| 4722 | User enabled | High |
| 4726 | User deleted | High |
| 4732 | Added to admin group | CRITICAL |

You do **not** need more at this stage.

---

## 4️⃣ Logon Types (THIS IS HUGE)

Event ID **4624 / 4625** has a field called **Logon Type**.

This tells you **HOW** the login happened.

### 🔹 MOST IMPORTANT LOGON TYPES

| Logon Type | Meaning | SOC Interpretation |
| --- | --- | --- |
| 2 | Interactive | Physical login |
| 3 | Network | SMB, remote access |
| 5 | Service | Service account |
| 7 | Unlock | Screen unlock |
| 10 | RemoteInteractive | **RDP login** |
| 11 | CachedInteractive | Offline login |

👉 **Logon Type 10 = RDP = HIGH ATTENTION**

---

## 5️⃣ SOC INVESTIGATION EXAMPLE

Alert:

> “Multiple failed logons detected”
> 

SOC steps:

1. Open Event Viewer
2. Filter Event ID **4625**
3. Check:
    - Username
    - Source IP
    - Logon Type

If:

- Logon Type = 10
- Username = Administrator
- Many failures

👉 **Brute-force attempt**

---

## 6️⃣ How to Filter Logs (PRACTICAL)

In Event Viewer:

- Security log
- Right-click → **Filter Current Log**
- Enter:

```
4624,4625
```

This is the Windows equivalent of:

```bash
grep"Failed password"
```

---

## 7️⃣ What We Are NOT Doing Yet

❌ Active Directory logons

❌ Kerberos deep dive

❌ Domain controllers

❌ SIEM correlation

Stored for later phases.

---

# 📘 SUMMARY TABLE (ADD TO NOTES)

| Item | Meaning |
| --- | --- |
| Local user | Machine-level account |
| Administrator | High-privilege |
| Event ID 4720 | User created |
| Event ID 4732 | Added to admin group |
| Logon Type 10 | RDP login |
| Logon Type 3 | Network login |

## 🧠 Lesson 3: Processes, Services & Malware Execution (CRITICAL)

Most real-world compromises are detected by:

> **“Something ran that shouldn’t have.”**
> 

This lesson teaches you **how SOC analysts detect that**.

---

## 1️⃣ What Is a Process? (SOC Definition)

A **process** = a running program.

Examples:

- `chrome.exe`
- `powershell.exe`
- `cmd.exe`
- `svchost.exe`

SOC analysts care about:

- **What ran**
- **Who ran it**
- **From where**
- **What it spawned**

---

## 2️⃣ Where to See Processes (Two Ways)

### 🔹 Task Manager (Quick View)

- Press **Ctrl + Shift + Esc**
- Go to **Processes** tab

SOC use:

- Spot suspicious names
- Spot high CPU/memory usage

But **Task Manager is NOT enough**.

---

## 3️⃣ MOST IMPORTANT PROCESS LOG: Event ID 4688

Event ID **4688** = **Process Creation**

This is the Windows equivalent of:

```bash
ps aux + audit
```

SOC goldmine.

---

### How to find it:

1. Event Viewer
2. Windows Logs → Security
3. Filter Event ID:

```
4688
```

---

## 4️⃣ What to Look for in Event ID 4688

Inside a 4688 event, focus on:

| Field | Why it matters |
| --- | --- |
| New Process Name | What executable ran |
| Creator Process | Parent process |
| Account Name | Who ran it |
| Process Command Line | Malware arguments |

---

## 5️⃣ SOC RED FLAGS (MEMORIZE THESE)

🚨 **Very suspicious executions**:

| Process | Why |
| --- | --- |
| `powershell.exe` | Malware delivery |
| `cmd.exe` | Script execution |
| `wscript.exe` / `cscript.exe` | Script-based malware |
| `mshta.exe` | Living-off-the-land |
| `rundll32.exe` | DLL abuse |

These are called **LOLBins**.

---

## 6️⃣ Parent–Child Process Logic (CRITICAL)

SOC analysts ALWAYS ask:

> “Does this parent → child relationship make sense?”
> 

### Normal:

```
explorer.exe → chrome.exe
```

### Suspicious:

```
winword.exe → powershell.exe
```

That usually means:

- Malicious document
- Macro attack

---

## 7️⃣ Services vs Processes (Know the Difference)

### 🔹 Process

- Runs when executed
- Can stop/start anytime

### 🔹 Service

- Runs in background
- Often auto-starts
- Used for persistence

---

### Where to view services:

- Press **Win + R**
- Type:

```
services.msc
```

SOC checks:

- Unknown services
- Services running as SYSTEM
- Recently installed services

---

## 8️⃣ SOC Mini Investigation Example

Alert:

> “Suspicious PowerShell execution”
> 

Steps:

1. Filter Event ID **4688**
2. Look for `powershell.exe`
3. Check:
    - Parent process
    - Command line
    - User
4. Decide:
    - Admin task? → false positive
    - From Word / Temp folder? → threat

---

## 9️⃣ What We Are NOT Doing Yet

❌ Sysmon

❌ PowerShell deep logging

❌ SIEM correlation

❌ Threat hunting

All stored for later.

---

# 📘 SUMMARY TABLE (ADD TO NOTES)

| Item | Meaning |
| --- | --- |
| Event ID 4688 | Process creation |
| Parent process | Who launched it |
| LOLBins | Legit tools abused |
| services.msc | Background services |
| powershell.exe | High-risk process |

## 🧠 Lesson 4: Persistence Mechanisms (Registry & Scheduled Tasks)

This lesson explains **how attackers survive reboots**.

If you understand this, you understand **80% of Windows persistence alerts**.

---

## 1️⃣ What Is Persistence? (SOC Definition)

**Persistence = techniques used by attackers to stay on the system after reboot or logout.**

SOC question:

> “Why is this malware still here after restart?”
> 

Answer:

> **Persistence mechanism**
> 

---

## 2️⃣ MOST COMMON WINDOWS PERSISTENCE METHODS (ONLY WHAT YOU NEED)

We focus on **2 methods** (most common, most abused):

1. **Registry Run Keys**
2. **Scheduled Tasks**

That’s enough for SOC L1.

---

## 3️⃣ Registry Run Keys (VERY IMPORTANT)

### What is the Registry?

A database where Windows stores:

- Startup programs
- Configurations
- System behavior

Attackers abuse it.

---

### 🔹 Most Abused Registry Path

```
HKCU\Software\Microsoft\Windows\CurrentVersion\Run
```

Anything here:

- Runs **every time the user logs in**
- Very common malware persistence

---

## 4️⃣ SOC-Relevant Event IDs (Registry)

| Event ID | Meaning |
| --- | --- |
| 4657 | Registry value modified |
| 4688 | Process modifying registry |

You don’t need more.

---

## 5️⃣ How SOC Investigates Registry Persistence

SOC steps:

1. Alert fires: “Registry modification”
2. Check Event ID **4657**
3. Identify:
    - Registry path
    - Value name
    - Executable path
4. Ask:
    - Legit software?
    - Suspicious location? (Temp, AppData)

---

## 6️⃣ Scheduled Tasks (SECOND MOST ABUSED)

### What is a Scheduled Task?

- Runs a program:
    - At startup
    - At logon
    - At specific time

Attackers love it.

---

### Where to view scheduled tasks:

- Press **Win + R**
- Type:

```
taskschd.msc
```

SOC checks:

- Unknown task names
- Tasks running PowerShell
- Tasks running from Temp/AppData

---

## 7️⃣ Scheduled Task SOC Indicators

🚨 Red flags:

- Task runs `powershell.exe`
- Task created recently
- Task runs hidden scripts
- Task name mimics system task

---

## 8️⃣ SOC Investigation Example

Alert:

> “New scheduled task detected”
> 

Steps:

1. Open Task Scheduler
2. Check:
    - Task name
    - Trigger
    - Action (program path)
3. Correlate with:
    - Event ID 4688
    - User who created it
4. Decide:
    - Admin automation → OK
    - Random PowerShell → Threat

---

## 9️⃣ What We Are NOT Doing Yet

❌ Advanced registry forensics

❌ Autoruns tool

❌ SIEM correlation

❌ Persistence chaining

Stored for later.

---

# 📘 SUMMARY TABLE (ADD TO NOTES)

| Item | Meaning |
| --- | --- |
| Persistence | Survive reboot |
| Run key | Auto-start programs |
| HKCU Run | User startup |
| Event ID 4657 | Registry change |
| taskschd.msc | Scheduled tasks |

## 🧠 Lesson 5: Windows Logs SOC Analysts ACTUALLY Use (FINAL)

You are **not** a Windows admin.

You are **not** a Windows engineer.

You are a **SOC analyst**.

So we focus on **only the logs that matter**.

---

## 1️⃣ The Only Windows Logs You Must Care About (L1)

There are **hundreds** of Windows logs.

SOC L1 needs **only these**:

| Log | Why it matters | Priority |
| --- | --- | --- |
| Security | Logins, processes, privilege use | ⭐⭐⭐ |
| System | Services, startup, failures | ⭐⭐ |
| Application | App crashes (low SOC use) | ⭐ |

👉 **Security log = 80% of your job**

---

## 2️⃣ Security Log – What It Tells You

Security log answers **core SOC questions**:

- Who logged in?
- From where?
- What ran?
- Who created users?
- Who escalated privileges?

Key Event IDs (FINAL list):

| Event ID | Meaning |
| --- | --- |
| 4624 | Successful login |
| 4625 | Failed login |
| 4688 | Process creation |
| 4720 | User created |
| 4732 | Added to admin group |
| 4657 | Registry modified |

You do **NOT** need more right now.

---

## 3️⃣ System Log – When Things Break or Start

System log answers:

- Did a service fail?
- Did something auto-start?
- Did Windows reboot?

SOC use:

- Detect persistence
- Detect service abuse
- Detect system instability after malware

You mainly **correlate**, not deeply analyze.

---

## 4️⃣ Application Log – Lowest Priority

This log records:

- App crashes
- Software errors

SOC uses it:

- Only when malware crashes
- Or when correlating timelines

👉 Do not waste time here.

---

## 5️⃣ SOC Timeline Thinking (CRITICAL)

SOC analysts think in **time order**, not tools.

Example timeline:

1. Failed logins (4625)
2. Successful login (4624)
3. Suspicious process (4688)
4. Registry persistence (4657)

That tells a **story**.

This is what SOC interviews test.

---

## 6️⃣ What We Have NOW COMPLETED

You now understand:

✅ Windows authentication

✅ Users & logon types

✅ Process execution

✅ Persistence mechanisms

✅ SOC-relevant logs

This is **exactly** what a SOC L1 must know about Windows.

---

## 7️⃣ What We Are INTENTIONALLY NOT Doing

❌ Sysmon

❌ PowerShell logging

❌ SIEM ingestion

❌ Active Directory

❌ Memory forensics

All stored for later phases.

Nothing forgotten.

---

# 📘 FINAL WINDOWS SUMMARY TABLE (ADD TO NOTES)

| Area | What you learned |
| --- | --- |
| Event Viewer | Central Windows logs |
| Security Log | Logins & processes |
| Logon Types | RDP vs local |
| Event ID 4688 | Malware execution |
| Registry Run | Persistence |
| Scheduled Tasks | Persistence |

# 🟦 WINDOWS EVENT IDs – SOC L1 MASTER TABLE

## 🔐 AUTHENTICATION & USER ACTIVITY (MOST IMPORTANT)

| Event ID | Event Name | What it Means | SOC Use | Importance |
| --- | --- | --- | --- | --- |
| **4624** | Successful Logon | User logged in successfully | Identify valid access | ⭐⭐⭐ |
| **4625** | Failed Logon | Login attempt failed | Brute-force detection | ⭐⭐⭐ |
| **4634** | Logoff | User logged out | Session timeline | ⭐ |
| **4647** | User Initiated Logoff | User manually logged off | Session closure | ⭐ |
| **4672** | Special Privileges Assigned | Admin-level login | Privilege abuse | ⭐⭐⭐ |

---

## 👤 USER & GROUP MANAGEMENT (HIGH SEVERITY)

| Event ID | Event Name | What it Means | SOC Use | Importance |
| --- | --- | --- | --- | --- |
| **4720** | User Account Created | New local user created | Backdoor account | ⭐⭐⭐ |
| **4722** | User Account Enabled | Disabled account enabled | Suspicious access | ⭐⭐ |
| **4726** | User Account Deleted | Account removed | Covering tracks | ⭐⭐ |
| **4732** | Added to Admin Group | User added to local admin | Privilege escalation | ⭐⭐⭐ |

---

## ⚙️ PROCESS EXECUTION (MALWARE DETECTION CORE)

| Event ID | Event Name | What it Means | SOC Use | Importance |
| --- | --- | --- | --- | --- |
| **4688** | Process Creation | A program was executed | Malware execution | ⭐⭐⭐ |
| **4689** | Process Termination | Process exited | Timeline building | ⭐ |

---

## 🧬 REGISTRY & PERSISTENCE

| Event ID | Event Name | What it Means | SOC Use | Importance |
| --- | --- | --- | --- | --- |
| **4657** | Registry Value Modified | Registry changed | Persistence detection | ⭐⭐⭐ |
| **4656** | Registry Access Attempt | Registry accessed | Early indicator | ⭐ |

---

## 🛠️ SYSTEM & SERVICE ACTIVITY

| Event ID | Event Name | What it Means | SOC Use | Importance |
| --- | --- | --- | --- | --- |
| **7036** | Service State Changed | Service started/stopped | Suspicious services | ⭐⭐ |
| **7045** | New Service Installed | New service added | Malware persistence | ⭐⭐⭐ |

---

## 🧠 LOGON TYPES (INSIDE 4624 / 4625)

| Logon Type | Meaning | SOC Interpretation |
| --- | --- | --- |
| **2** | Interactive | Physical login |
| **3** | Network | SMB / network access |
| **5** | Service | Service account |
| **7** | Unlock | Screen unlock |
| **10** | RemoteInteractive | **RDP login (CRITICAL)** |
| **11** | CachedInteractive | Offline login |

---

## 🚨 TOP SOC ALERT COMBINATIONS (INTERVIEW GOLD)

| Pattern | What It Indicates |
| --- | --- |
| 4625 → 4624 | Successful brute-force |
| 4624 (Logon 10) | RDP access |
| 4688 (powershell.exe) | Script-based attack |
| 4720 + 4732 | Backdoor admin account |
| 4688 + 4657 | Malware persistence |
| 7045 + unknown service | Service-based malware |

# 🟦 SUMMARY TABLE 2: WINDOWS TOOLS & WHAT SOC USES THEM FOR

This connects **tool → purpose**, not admin usage.

| Tool | Command | SOC Use |
| --- | --- | --- |
| Event Viewer | `eventvwr.msc` | Log investigation |
| Task Manager | `taskmgr` | Live process view |
| Services | `services.msc` | Malicious services |
| Task Scheduler | `taskschd.msc` | Persistence detection |
| Local Users | `lusrmgr.msc` | Backdoor accounts |
| CMD | `cmd` | Investigation commands |
| PowerShell | `powershell` | Often abused |

# CIA TRAID

## 🧠 Lesson 0: CIA Triad (SOC Analyst Perspective)

This will be:

- Short
- Clear
- Interview-ready
- SOC-focused (not theory-heavy)

After that:

➡️ We immediately continue to **SOC Logs & SIEM**

---

## 🔐 CIA TRIAD – SIMPLE BUT POWERFUL

CIA = **what security is trying to protect**

| Letter | Meaning | Plain English |
| --- | --- | --- |
| **C** | Confidentiality | Only the right people see data |
| **I** | Integrity | Data is not altered |
| **A** | Availability | Systems/data are accessible |

---

## 🔎 CIA TRIAD FROM A SOC ANALYST VIEW

### 1️⃣ Confidentiality (MOST COMMON INCIDENT)

**Broken when:**

- Unauthorized access
- Data leak
- Credential theft

**SOC examples:**

- RDP login from unknown IP
- Admin account created secretly
- Database accessed by attacker

**Related alerts:**

- Event ID 4624 (suspicious login)
- Event ID 4720 (new user)
- Event ID 4732 (added to admin)

👉 SOC question:

> “Who accessed data that shouldn’t?”
> 

---

### 2️⃣ Integrity (SILENT BUT DANGEROUS)

**Broken when:**

- Files modified
- Registry altered
- System configs changed

**SOC examples:**

- Malware modifying registry run keys
- Scheduled task added
- Log files deleted or altered

**Related alerts:**

- Event ID 4657 (registry change)
- Event ID 4688 (process modifying system)

👉 SOC question:

> “What changed, and who changed it?”
> 

---

### 3️⃣ Availability (LOUD INCIDENTS)

**Broken when:**

- System is down
- Service crashes
- Resource exhaustion

**SOC examples:**

- DDoS attack
- Ransomware encrypts system
- Critical service stopped

**Related alerts:**

- Service stopped (System log)
- Reboot loops
- Resource spikes

👉 SOC question:

> “Is the business still operational?”
> 

---

## 🧠 HOW SOC USES CIA (VERY IMPORTANT)

SOC does **NOT** memorize CIA.

SOC uses it to **decide severity**.

| Incident | CIA Impact | Severity |
| --- | --- | --- |
| Failed login | None | Low |
| RDP access | Confidentiality | High |
| Registry persistence | Integrity | High |
| Ransomware | All three | Critical |

---

## 🎯 INTERVIEW-READY ANSWER (MEMORIZE THIS)

> “The CIA triad represents confidentiality, integrity, and availability.
> 
> 
> As a SOC analyst, I use it to assess the impact and severity of incidents.
> 
> For example, unauthorized logins affect confidentiality, registry persistence affects integrity, and DDoS or ransomware affects availability.”
>
