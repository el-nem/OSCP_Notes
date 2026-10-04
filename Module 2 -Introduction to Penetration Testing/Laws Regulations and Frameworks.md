# Laws, Regulations, and Frameworks

---

## Authorization and Scope

Legal authorization is what separates penetration testing from a crime. Before any technical testing begins, an engagement requires:
- **Written authorization** and a signed **Statement of Work (SoW)**
- **Rules of Engagement (RoE)** — defines timing, allowed techniques, emergency contacts
- A clearly defined **scope** — exactly which systems/networks/IP ranges are approved for testing

Testing outside agreed scope — even accidentally — carries real legal risk, regardless of intent. This is the first and most important concept in any professional testing engagement, well before any technical methodology.

*(See your PTES / Pre-Engagement notes for the full breakdown of NDA types, scoping questionnaires, and RoE components.)*

---

## Computer Crime Laws

Written authorization protects me from these laws. Without it, testing = a crime in most countries. Always check the exact law before working in a country *(verify the details, laws change)*.

- **Germany:** `StGB §202a` (data espionage = accessing protected data without permission), `§202b` (intercepting data), `§202c` (preparing these crimes, like making or sharing tools/passwords for them. Dual-use tools like Nmap are a grey area, intent matters), `§303b` (computer sabotage)
- **Spain:** `Código Penal Art. 197 bis` (unauthorized access to information systems)
- **UK:** `Computer Misuse Act 1990`
- **US:** `CFAA` (Computer Fraud and Abuse Act)
- **Egypt:** `Law No. 175 of 2018` (Anti-Cyber and Information Technology Crimes Law)

---

## Regional Compliance Requirements Requiring Penetration Testing

**United States**
- `PCI DSS` — mandates annual penetration testing for organizations processing card payments
- `HIPAA` — indirectly requires penetration testing through its risk assessment stipulations for healthcare entities
- `SOC 2` — encourages penetration testing to validate effectiveness of implemented security controls
- `GLBA` (under FTC rules) — specifically requires financial institutions to conduct penetration tests annually

**European Union**
- `GDPR` — necessitates regular testing of security measures, typically including penetration testing for data protection compliance
- `NIS Directive` — implies the need for penetration testing to manage security risks effectively (see NIS2 note below for the current version)

**United Kingdom**
- `Data Protection Act 2018` — aligns with GDPR, suggesting penetration testing for assessing security measures
- `DSP Toolkit` (healthcare) — recommends penetration testing for compliance with data security standards

**India**
- `RBI-ISMS` — requires banks and financial institutions to perform penetration testing for compliance

**Brazil**
- `LGPD` — implies the necessity of penetration testing to ensure security of personal data

---

## NIS2

- `NIS2` = the newer version of the NIS Directive (EU 2022/2555). It replaced NIS1
- EU countries had to turn it into national law by October 2024, but not all were on time ⇒ check the status for Germany and Spain before working there
- Covers more sectors than NIS1 (energy, transport, health, digital infrastructure, etc.)
- Main requirements: risk management measures, incident reporting (early warning within 24 hours), and top management is responsible

---

## NIST (National Institute of Standards and Technology)

- **NIST Cybersecurity Framework (CSF):** A voluntary framework for managing cybersecurity risks
- **NIST SP 800-53:** Catalog of security and privacy controls for federal information systems
- **NIST SP 800-171:** Focuses on protecting Controlled Unclassified Information (CUI) in non-federal systems
- **NIST SP 800-115:** "Technical Guide to Information Security Testing and Assessment" — not strictly a pentest methodology, but valuable guidance on security assessment planning, execution, and post-testing activities. Especially relevant when working with government agencies or NIST-aligned organizations.
- **NIST SP 800-61:** Guidelines for incident handling and response (preparation, detection, analysis, containment, eradication, recovery) *(see `Incident Response Lifecycle`)*

Reference: https://www.nist.gov/privacy-framework/nist-sp-800-115

---

## ISO/IEC 27001

- Specifies requirements for establishing, implementing, and maintaining an **Information Security Management System (ISMS)**
- **ISO/IEC 27002:** Provides guidelines for implementing the security controls ISO 27001 outlines
- **ISO/IEC 27035:** Standard for information security incident management — focuses on incident response planning and execution

---

## PCI DSS (Payment Card Industry Data Security Standard)

- A set of security standards protecting payment card data
- Applies to any organization handling credit card transactions
- Requires organizations to conduct regular penetration tests — **at least annually**, and after any significant infrastructure or application change
- Requirements include encryption, access control, and regular security testing

Reference: https://www.pcisecuritystandards.org/

---

## GDPR (General Data Protection Regulation)

- EU regulation governing data protection and privacy for individuals within the EU
- Focuses on **consent, data minimization, and the right to be forgotten**
- Applies to organizations processing EU citizens' data **regardless of where the organization itself is located** — directly relevant when working with German/Spanish clients or data
- Doesn't explicitly mandate "penetration testing" by name, but regular security testing is considered a best practice for demonstrating GDPR compliance

Reference: https://gdpr-info.eu/

---

## Core Penetration Testing Methodologies (supporting context)

- **PTES (Penetration Testing Execution Standard)** — 7 phases: Pre-engagement Interactions, Intelligence Gathering, Threat Modeling, Vulnerability Analysis, Exploitation, Post-Exploitation, Reporting *(see dedicated PTES notes for full detail)*
- **NIST SP 800-115** — formal technical guide to security assessment, especially relevant for government-aligned work
- **OWASP Testing Guide** — web application testing methodology. It is split into test categories (Information Gathering, Configuration and Deployment Management, Identity Management, Authentication, Authorization, Session Management, Input Validation, Business Logic, Client-side, API, etc.), with practical examples for nearly every web vulnerability class; community-maintained and continuously updated
- **MITRE ATT&CK** — adversary tactics/techniques knowledge base used to simulate realistic threat scenarios *(see Cybersecurity Strategies notes for full detail)*

---

## Other Frameworks Referenced (Context, Broader Than This Module)
- **HIPAA** — US healthcare data protection
- **FISMA** — US federal agency cybersecurity requirements
- **SOX (Sarbanes-Oxley)** — US financial transparency/accountability for public companies
- **COPPA** — US children's online privacy protection
- **CCPA** — California Consumer Privacy Act
- **CIS Controls** — 18 prioritized critical security actions
- **COBIT** — IT governance and management framework

---
