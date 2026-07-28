# Penetration Testing Process

Difficulty: Easy
Platform: General
Status: Solid
Type: Concept

# Pre-Engagement interactions

During this phase, we define :

1. Kick-off meeting with the client.
2. Scope ⇒ what is in scope and what is out of scope. 
3. How long the engagement will realistically take based on scope size.
4. Dealing with third parties.
5. What’s allowed if social engineering is in scope?
6. Payment terms
7. Emergency contact information → if something breaks or a critical vuln is found mid-test
8. NDA (Non-Disclosure Agreement)
    - *Unilateral NDA:* only one party is obligated to maintain confidentiality
    - *Bilateral NDA:* both parties obligated — most common type for pentest engagements
    - *Multilateral NDA:* three or more parties bound — used when multiple organizations are involved (e.g., testing shared/cooperative infrastructure)
9. Rules of Engagement (RoE) — timing, allowed techniques, emergency contacts.
10. Getting written authorization and Statement of Work (SoW).

---

# Intelligence gathering

In this phase, we collect information about the target system via 3 ways :

- **Active Recon:** Directly interacting with the target to elicit information from it, such as ping sweeps or port scans.
- **Passive Recon:** This is when information is gathered without having any direct interaction with the target. This would include *includes* OSINT (WHOIS, social media, public records) as its main technique
    - **Open Source Intelligence (OSINT):** Exploiting open-source data to develop an understanding of the target, such as from company websites or forums.

---

# Threat Modeling

In this phase, we use intelligence gathered to identify and prioritize realistic attack vectors and high-value assets, based on business impact and threat-actor motivation — not just technical exploitability.

**Core process:**

- Identify business assets (data, systems, intellectual property) and their relative value
- Identify business processes that depend on those assets.
- Map threat communities/actors relevant to the organization (e.g., competitors, insiders, opportunistic attackers, organized crime, nation-state — depending on the client's industry and profile)
- Match threat actors to threat capability and likely motivation
- Prioritize attack vectors based on likelihood **and** consequence, not just ease of exploitation.

---

# **Vulnerability Analysis**

In this phase, take the data that we collect from scanners and the data that we enumerate from Intelligence gathering to identify security flaws and prioritize them before starting the exploitation phase. 

**Core activities:**

- **Active scanning** — automated vulnerability scanners (Nessus, OpenVAS, Nmap NSE scripts) against in-scope targets
- **Manual inspection** — reviewing configurations, code, and service behavior that scanners miss or misjudge
- **Service enumeration** — deep-diving each discovered service to confirm version, configuration, and known weaknesses
- **Validation** — confirming that a flagged "vulnerability" is real and not a false positive before treating it as an attack vector
- We create a validated list of exploitable weaknesses, correlated back to the assets and attack vectors prioritized in the Threat Modeling phase.

---

# Exploitation

In this phase, we exploit a vulnerability we found and try to bypass security controls in the system to gain full access or to see what real damage the vulnerability would cause if a real hacker used it to attack our customer's system.

**Core activities:**

- Preparing exploit code, tools, and environment ahead of the live attempt (test in a lab/sandbox where possible before firing at production)
- Choosing between public exploits (adapted as needed) and custom/manual exploitation
- Careful, controlled execution
- Establishing initial access (shell, credentials, or another form of foothold)

---

# Post-Exploitation

In this phase, when we get initial access to the system, we see the machine that we access, and if it does not have privileges, try to escalate privileges and get access to other machines on the system 

**Core activities:**

- Moving inside the network from the initial foothold (lateral movement across systems)
- Raising privilege levels (local and/or domain privilege escalation)
- Assessing the value of accessed data — what's actually sensitive/damaging if this had been a real attacker
- Identifying persistence opportunities (only if authorized — many engagements explicitly exclude leaving backdoors)
- Mapping how far a real attacker could have gone from this single point of entry

---

# Reporting

In this phase, we write all technical findings, exploits, and post-exploit successes into a structured document that helps the customer understand their risk. We should give POCs and cases, and how customers can solve these findings and wht is finacial and operaonal risk

**Core components:**

- **Executive Summary** — non-technical, business-risk framed, written for leadership who won't read the technical detail
- **Technical Report** — full findings with reproduction steps, evidence (screenshots/logs), risk ratings, and specific remediation guidance
- Findings should flow logically from earlier phases — intelligence gathered in Phase 2 should visibly inform the threat modeling in Phase 3 and the exploitation narrative in Phase 5, so nothing feels disconnected or dropped
- Reports are typically written for **multiple audiences** at once: leadership (risk/business impact), engineering (technical remediation), and sometimes audit/compliance teams (control mapping)