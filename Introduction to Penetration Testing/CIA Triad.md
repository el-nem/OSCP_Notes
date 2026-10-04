# The CIA Triad

The CIA Triad is a foundational concept in information security, representing the three core principles of security: **Confidentiality**, **Integrity**, and **Availability**. It's a framework for evaluating and implementing security measures — sometimes referenced as the AIC triad.

---

## Confidentiality
Ensures that sensitive information is accessed only by authorized individuals, systems, or processes. Protects data from unauthorized disclosure.

**Key Concepts:**
- **Encryption:** Protects data at rest, in transit, and in use (e.g., AES, RSA)
- **Access Controls:** Mechanisms like passwords, biometrics, and role-based access control (RBAC) restrict access to sensitive data
- **Data Masking:** Hides sensitive data (e.g., replacing credit card numbers with asterisks)
- **Steganography:** Hides data within other files (e.g., images or audio files)

**Examples:**
- Encrypting emails to prevent unauthorized access
- Using multi-factor authentication (MFA) to secure user accounts

**Threats to Confidentiality:**
- Eavesdropping attacks
- Man-in-the-middle (MITM) attacks
- Social engineering (e.g., phishing)

**Attack Example:** A man-in-the-middle attack intercepts unencrypted traffic between a user and server, exposing login credentials — this violates confidentiality.

---

## Integrity
Ensures that data is accurate, consistent, and trustworthy throughout its lifecycle. Protects data from unauthorized modification.

**Key Concepts:**
- **Hashing:** Verifies data integrity (e.g., SHA-256). MD5 is broken (collisions), so don't use it for security, only for basic checksums
- **Digital Signatures:** Ensures authenticity and integrity of data
- **Checksums:** Detects errors or changes in data
- **Version Control:** Tracks changes to files or systems

**Examples:**
- Using hashes to verify that a file has not been tampered with
- Implementing change management processes to track system updates

**Threats to Integrity:**
- Data tampering by malicious actors
- Unauthorized system changes

**Attack Example:** A hacker alters the contents of a financial transaction without authorization before it's processed — this violates integrity.

---

## Availability
Ensures that systems and data are accessible and operational when needed by authorized users.

**Key Concepts:**
- **Redundancy:** Duplicating systems or data to ensure uptime (e.g., RAID, failover clusters)
- **Backups:** Regularly saving data to restore it in case of loss or corruption
- **Disaster Recovery Plans (DRP):** Procedures to recover systems after an incident
- **Load Balancing:** Distributing traffic across multiple servers to prevent overload

**Examples:**
- Using uninterruptible power supplies (UPS) to maintain power during outages
- Implementing distributed denial-of-service (DDoS) protection to ensure website availability

**Threats to Availability:**
- DDoS attacks overwhelming systems
- Hardware failures or natural disasters
- Ransomware encrypting files and locking users out of systems (main impact = availability)

**Attack Example:** A DDoS attack overwhelms a company's website with traffic, making it inaccessible to legitimate users — this violates availability.

---

## Quick Reference: Attack → Principle Violated
| Attack | Principle Violated |
|---|---|
| Man-in-the-middle (MITM) | Confidentiality |
| Eavesdropping | Confidentiality |
| Phishing (credential theft) | Confidentiality |
| Ransomware (encrypts files, locks access) | Availability (also Confidentiality if data is stolen first = double extortion) |
| Unauthorized data tampering | Integrity |
| DDoS | Availability |
| Hardware failure / natural disaster | Availability |

---
