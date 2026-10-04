# Security Principles and Controls

Security controls are measures or mechanisms implemented to protect the confidentiality, integrity, and availability (CIA) of information systems and data. They are designed to prevent, detect, and respond to security threats, vulnerabilities, and risks.

---

## Core Security Principles

### Least Privilege

A security best practice where users are granted only the minimum permissions necessary to perform their job functions. This limits potential damage from malicious software, compromised accounts, or user errors. Access provisioning should align permission levels directly with job roles rather than granting broad access "just in case."

### Defense in Depth

Implementing **multiple layers** of security controls rather than relying on a single control. If one layer fails or is bypassed, additional layers still provide protection. This is the correct concept whenever a question describes "using several different types of controls together" rather than one single safeguard.

---

## Categories of Security Controls

- **Technical Controls** — implemented through technology to automate security processes
  - Examples: Firewalls, intrusion detection systems (IDS), antivirus software, encryption, access control mechanisms
- **Managerial Controls** — policies, procedures, and guidelines to manage and supervise information systems
  - Examples: Security training, contingency planning, risk assessments, compliance policies
- **Operational Controls** — implemented by people rather than automated systems
  - Examples: Security guards, user management, incident response procedures, change management
- **Physical Controls** — protect physical assets like facilities and hardware
  - Examples: Locks, alarms, surveillance cameras, badge readers

---

## Functional Types of Security Controls

| Type             | Purpose                                                                     | Examples                                                                 |
| ---------------- | --------------------------------------------------------------------------- | ------------------------------------------------------------------------ |
| **Preventive**   | Prevent security incidents before they occur                                | Firewalls, antivirus software, access control mechanisms, IPS            |
| **Detective**    | Identify and document attempted or successful intrusions                    | IDS, log monitoring, audits, CCTV                                        |
| **Corrective**   | Mitigate damage or restore systems after a breach                           | Backup and restore procedures, patch management, incident response plans |
| **Deterrent**    | Discourage attackers psychologically rather than physically blocking access | Warning signs, security policies, visible security personnel             |
| **Compensating** | Alternative controls used when primary controls aren't feasible             | Additional monitoring, manual processes in place of automated tools      |
| **Directive**    | Direct or confine actions to enforce compliance with security policies      | Security policy statements, signs, guardrails                            |

---

## Category × Type Examples Table

| Category / Type | Preventive                        | Deterrent                       | Detective                        | Corrective                 | Compensating                       | Directive                      |
| --------------- | --------------------------------- | ------------------------------- | -------------------------------- | -------------------------- | ---------------------------------- | ------------------------------ |
| **Technical** | Intrusion Prevention System (IPS), encryption of sensitive data, biometric access control | Login warning banner (monitoring notice) | Intrusion Detection System (IDS) | Patch management system | Virtual Private Network (VPN) | Access control policies |
| **Managerial** | Security awareness training, background checks for employees | Disciplinary action in security policy | Regular security audits | Incident response plan | Job rotation policies | Data classification policies |
| **Operational** | Security guards checking IDs at the door | Security cameras | Security guard patrols | Emergency response drills, restoring from backups | Multi-factor authentication | Employee security training |
| **Physical**    | Security turnstiles               | Fencing with barbed wire        | CCTV surveillance                | Sprinkler system for fires | Uninterruptible Power Supply (UPS) | Sign: "No Unauthorized Access" |

---

> Note: some examples can fit more than one type. For the exam, learn what each type does (first table) more than the cells.

---

## Access Control Models (Supporting Context)

| Model                                     | Controlled By      | Flexibility  | Security  | Use Case                                                                                                            |
| ----------------------------------------- | ------------------ | ------------ | --------- | ------------------------------------------------------------------------------------------------------------------- |
| **MAC** (Mandatory Access Control)        | Admin              | Low          | High      | Military/Government — resources labeled by security level (confidential, secret, top secret)                        |
| **DAC** (Discretionary Access Control)    | Data Owner         | High         | Moderate  | Small teams/personal use — e.g., a shared spreadsheet with owner-set permissions                                    |
| **RBAC** (Role-Based Access Control)      | Admin (Groups)     | Moderate     | High      | Corporate environments — access tied to job role/group membership                                                   |
| **Rule-Based Access Control**             | Admin (Rules)      | Low-Moderate | High      | Time/context-sensitive — e.g., lab data accessible only 9am-5pm                                                     |
| **ABAC** (Attribute-Based Access Control) | Admin (Attributes) | High         | Very High | Dynamic/complex policies — e.g., access granted only to Engineering role, during business hours, from corporate IPs |

### Network Access Control (NAC)

Ensures devices meet security standards before granting network access:

- **Compliance Checks** — verifies OS version, patch level, antivirus status
- **Dynamic VLAN Assignment** — assigns VLANs based on user identity, device type, or location
- **Agent-Based vs. Agentless** — agent-based uses installed software; agentless relies on network scans or DHCP fingerprinting

### Best Practices

- **Fail-Closed vs. Fail-Open:** Logical security controls (firewalls) should `fail closed` (also called fail-secure) → if they break, they block access, so no unauthorized access. Safety controls (like fire exit doors) should `fail open` so people can get out. Some books call fail-open for safety "fail-safe", so read the question carefully
- Conduct regular audits of access control policies
- Train users on secure practices

---
