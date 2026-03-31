# EXECUTION (MITRE TACTIC)

---

# What is Execution?

## Technical Definition

Execution is the stage where an attacker **runs malicious code on a system** after gaining access.

This could include:

- Running malware
- Executing scripts
- Launching malicious commands
- Using built-in system tools to run payloads

Execution is important because **attacks become active only after code runs**.

Access alone does not damage the system.

Execution allows the attacker to start controlling the system.

---

## Simple Explanation

If hacking is like breaking into a house:

Initial Access = thief enters the house

Execution = thief starts opening drawers and safes

The attacker is now **doing things inside the system**.

---

# Why Execution Matters in SOC

Most security alerts appear at the **Execution stage**.

Because:

Running programs leaves traces such as:

- process creation logs
- command line logs
- script execution logs

SOC analysts often detect attacks here.

---

# Common Execution Techniques

We focus only on SOC-relevant ones.

---

# 1️⃣ PowerShell Execution

Attackers often run malicious commands using PowerShell.

Example:

```
powershell -EncodedCommand <base64 code>
```

Why attackers use it:

- PowerShell exists on every Windows machine
- Can download malware
- Can execute scripts silently

---

### SOC Logs

Windows Event ID:

4688 → process creation

Example log:

```
powershell.exe -EncodedCommand aW52b2tl...
```

Encoded commands are major red flags.

---

# 2️⃣ Command Prompt Execution

Attackers use command prompt to run system commands.

Example:

```
cmd.exe
```

They may run:

```
net user
net group
whoami
```

These commands help them control the system.

---

### SOC Logs

Process creation logs show:

```
cmd.exe
```

Check command line arguments.

---

# 3️⃣ Malware Execution

Attackers may run:

```
malware.exe
trojan.exe
payload.exe
```

This allows:

- remote access
- data theft
- ransomware

---

### SOC Logs

You may see:

- unknown executable names
- execution from suspicious folders

Example:

```
C:\Users\Public\svchost.exe
```

Legitimate svchost never runs from there.

---

# 4️⃣ Living Off The Land (LOLBins)

Attackers use **legitimate Windows tools for malicious actions**.

Examples:

- powershell
- rundll32
- mshta
- wmic

Why?

Security tools trust these programs.

So attackers hide inside them.

---

# SOC Relevance

Execution stage helps detect:

- malware activity
- attacker commands
- persistence creation
- credential dumping
- lateral movement

Many SOC alerts trigger here.

---

# Real Industry Example

Alert shows:

```
4688 → powershell.exe -EncodedCommand
4688 → rundll32.exe malicious.dll
```

MITRE mapping:

Execution → PowerShell

Execution → Rundll32

Next stage could be:

Command and Control

---

# How SOC Analysts Investigate Execution

You check:

1️⃣ What process started?

2️⃣ Who started it?

3️⃣ Parent process?

4️⃣ Command line arguments?

5️⃣ Was this normal for that user?

Context matters.

---

# Common Beginner Mistakes

❌ Thinking PowerShell is always malicious

❌ Ignoring command arguments

❌ Ignoring parent process

❌ Not checking what happened after execution

Execution alone is suspicious.

But context determines incident.
