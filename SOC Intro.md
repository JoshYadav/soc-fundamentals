# Phase 2 - Core SOC

## Module 1: How a SOC Actually Works (Real Industry View)

Most students think SOC = watching dashboards.

Wrong.

SOC = decision engine.

---

# 1️⃣ What is a SOC? (Interview-Ready Answer)

### Simple Version (30 sec)

A Security Operations Center (SOC) is a centralized team that monitors, detects, investigates, and responds to security threats in real time using logs, alerts, and security tools.

### Technical but Clear Version (2 min)

A SOC is a structured security team responsible for continuous monitoring of an organization’s infrastructure. It collects logs from endpoints, servers, firewalls, cloud systems, and applications into centralized monitoring systems like SIEM. Analysts investigate alerts, determine whether they are false positives or real threats, assess severity, and either contain the threat or escalate it to higher tiers.

Good SOC work is not about tools — it’s about analysis, correlation, and decision-making.

Memorize structure, not wording.

---

# 2️⃣ SOC Tier Model (Very Important)

You must understand your future role clearly.

---

## 🔹 SOC L1 (You are training for this)

Role:

- Monitor alerts
- Perform initial investigation
- Validate false positive vs real threat
- Gather evidence
- Escalate when needed
- Document findings

L1 does NOT:

- Perform deep malware reverse engineering
- Design detection rules
- Perform enterprise-wide hunting

L1 answers:

> “Is this alert real, and what happened?”
> 

---

## 🔹 SOC L2

Role:

- Deep investigation
- Threat hunting
- Advanced log correlation
- Detection tuning
- Rule improvement
- Reduce false positives

L2 answers:

> “How did this attack happen and how do we prevent similar ones?”
> 

---

## 🔹 SOC L3

Role:

- Malware analysis
- Incident response leadership
- Threat intelligence
- Detection engineering
- Strategic defense improvement

L3 answers:

> “How do we stop this class of attack permanently?”
> 

---

If interviewer asks:

"What is difference between L1 and L2?"

Correct answer structure:

L1 performs alert triage and initial investigation. L2 performs deeper forensic analysis, correlation across multiple systems, and improves detection rules based on findings.

---

# 3️⃣ Alert vs Event vs Incident (Deep Understanding)

You MUST never confuse these.

---

### Event

A single log entry.

Example:

Event ID 4625 — failed login attempt.

---

### Alert

A triggered notification based on predefined rule.

Example:

10 failed logins within 1 minute triggers brute force alert.

Alert = suspicion.

Not proof.

---

### Incident

Confirmed malicious activity that impacts security.

Example:

Successful brute force → new admin account created → persistence established.

That is incident.

---

Interview Trap:

If interviewer asks:

“Is every alert an incident?”

Correct answer:

No. Alerts are rule-based triggers. Many alerts are false positives. An incident is confirmed malicious activity after investigation.

If you say yes → you fail.

---

# 4️⃣ Alert Lifecycle (Very Important)

When an alert appears:

You must think in this order:

1. What rule triggered it?
2. What logs support it?
3. Is pattern suspicious?
4. Was there success?
5. What happened after?
6. What is business impact?
7. What severity?
8. Escalate or close?

Memorize this investigation backbone.

This is your brain framework.

---

# Now We Test You

Scenario:

Alert Name: "Multiple Failed Login Attempts"

You open logs and see:

- 4625 from IP 10.10.5.4 (user: hr_user)
- 4625 from same IP
- 4625 from same IP
- 4624 (success) from same IP
- 4688 (powershell.exe launched)
- 4688 (net user newadmin /add)
- 4732 (newadmin added to administrators group)

Answer in structured format:

1. What happened?
2. Is this alert or incident?
3. What stage is attacker in?
4. What severity level?
5. What should L1 do next?

New scenario:

Windows logs show:

- 4624 (logon type 3) from IP 192.168.10.8 for user finance_user
- 4688 → powershell.exe -EncodedCommand ...
- 4688 → rundll32.exe suspicious.dll
- 5156 → outbound network connection to 185.234.219.10
- No failed login attempts before this

Answer in full structured format:

1. What likely happened?
2. What makes this suspicious?
3. What attack stage might this be?
4. Severity?
5. What should L1 check next?

# 🔵 MITRE ATT&CK FRAMEWORK

---

## What is MITRE ATT&CK?

MITRE ATT&CK is a **knowledge framework** that categorizes how attackers behave during cyber attacks.

It does NOT describe malware names.

It describes attacker behavior.

Think of MITRE as:

> A rulebook of real-world hacking techniques.
> 

---

## Why MITRE is Needed

Without MITRE:

- Analysts describe attacks randomly
- Reports are inconsistent
- No structured language

With MITRE:

- Every attack is mapped to a known behavior
- Investigations become standardized
- SOC teams speak a common language

---

## Core Structure of MITRE

MITRE has two main components:

### 🔹 Tactic

A **tactic** represents the attacker’s goal.

Example goals:

- Get access
- Stay inside
- Steal data
- Move to another system

Think of tactic as:

> What the attacker wants to achieve
> 

---

### 🔹 Technique

A **technique** is the method used to achieve that goal.

Example:

- Brute force
- Phishing
- Scheduled task creation
- PowerShell execution

Think of technique as:

> How the attacker achieves the goal
> 

---

## Example

If attacker tries many passwords:

Tactic: Initial Access

Technique: Brute Force

If attacker creates new admin account:

Tactic: Persistence

Technique: Create Account

---

## Common Attack Flow (MITRE View)

Most attacks follow stages like:

1️⃣ Initial Access

2️⃣ Execution

3️⃣ Persistence

4️⃣ Privilege Escalation

5️⃣ Defense Evasion

6️⃣ Credential Access

7️⃣ Discovery

8️⃣ Lateral Movement

9️⃣ Command and Control

🔟 Exfiltration

1️⃣1️⃣ Impact

Not all attacks use every stage.

But most follow this progression.

---

## Real SOC Example

Alert shows:

- Multiple failed logins
- Then successful login
- Then new admin user created

MITRE mapping:

- Failed logins → Initial Access (Brute Force)
- Successful login → Initial Access succeeded
- New admin account → Persistence
- Added to admin group → Privilege Escalation

Now investigation is structured.

---

## SOC Relevance

MITRE helps you:

- Describe attack stage clearly
- Write professional reports
- Escalate intelligently
- Reduce vague explanations

Interview question:

“How would you describe this attack?”

Weak answer:

“Someone hacked.”

Strong answer:

“This activity aligns with Initial Access via Brute Force, followed by Persistence through account creation.”

That is hireable language.

---

## Common Beginner Mistake

❌ Thinking MITRE is a tool

❌ Trying to memorize all technique IDs

❌ Ignoring attack progression

You only need:

- Understand stages
- Recognize patterns
- Map logically
