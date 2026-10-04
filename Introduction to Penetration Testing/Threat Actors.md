# Threat Actors

Threat actors are individuals or groups responsible for cybersecurity incidents, such as data breaches, malware distribution, or system compromises. They vary in skill level, motivation, and resources.

---

## Types of Threat Actors

### Nation-State Actors
- **Description:** Highly skilled attackers sponsored by governments for cyber espionage, warfare, or disruption of critical infrastructure
- **Resources:** Extensive funding and access to advanced tools (custom malware, zero-day exploits)
- **Motivations:** Political, philosophical, or strategic goals — disrupting enemy infrastructure, stealing classified information
- **Example:** Stuxnet, widely attributed to the U.S. and Israel (never officially confirmed), used to target Iranian nuclear facilities
- **Key trait:** Associated with APTs (Advanced Persistent Threats) — characterized by **long-term persistence and stealth**, not short smash-and-grab attacks

### Unskilled Attackers (Script Kiddies)
- **Description:** Individuals with limited technical expertise who rely on pre-made scripts or tools
- **Resources:** Minimal funding, basic tools only
- **Motivations:** Curiosity, disruption, minor financial gain
- **Example:** Launching DDoS attacks using readily available tools
- **Key trait:** Rely entirely on pre-made tools/scripts — do not develop custom malware

### Hacktivists
- **Description:** Technologically skilled individuals or groups motivated by political, social, or environmental ideologies
- **Resources:** Moderate funding, often through donations or crowdfunding
- **Motivations:** Promoting a cause — exposing unethical practices, defacing websites
- **Example:** The Anonymous group, known for high-profile attacks against organizations perceived as unethical

### Organized Crime
- **Description:** Well-structured groups focused on financial gain through cybercrime
- **Resources:** High funding, often with a corporate-like structure (developers, exploit managers, customer support)
- **Motivations:** Profit through ransomware, identity theft, data breaches
- **Example:** Ransomware attacks targeting businesses for extortion

### Insider Threats
- **Description:** Individuals within an organization who misuse their access for malicious purposes
- **Resources:** Access to internal systems and data
- **Motivations:** Financial gain, revenge, or carelessness
- **Example:** An employee leaking sensitive data to a competitor
- **Key trait:** Dangerous precisely because they already have legitimate access — no perimeter to breach

### Shadow IT
- **Description:** Departments or individuals using unauthorized IT systems or software, bypassing organizational policies
- **Resources:** Limited budget, often personal credit cards for cloud services
- **Motivations:** Convenience or frustration with IT restrictions
- **Example:** A team using unapproved cloud storage for sensitive data

---

## Comparison Table

| Threat Actor | Location | Resources | Sophistication | Possible Motivation |
|---|---|---|---|---|
| Nation-States | External | Extensive | Very High | Data exfiltration, philosophical, revenge, disruption, war |
| Unskilled Attackers | External | Limited | Very Low | Data exfiltration, sometimes philosophical, disruption |
| Hacktivists | External | Some funding | Can be high | Philosophical, disruption, revenge, chaos |
| Insider Threat | Internal | Many resources (internal access) | Medium | Revenge, financial gain |
| Organized Crime | External | Often extensive | Very High | Financial |
| Shadow IT | Internal | Limited | Low | Convenience, frustration with IT rules |

---

## Motivations of Threat Actors (Summary)
- **Data Exfiltration** — stealing sensitive information for espionage or resale
- **Financial Gain** — profiting through ransomware, fraud, identity theft
- **Service Disruption** — causing chaos or demanding ransom via service disruption
- **Philosophical/Political Beliefs** — promoting ideologies through hacktivism
- **Revenge** — targeting organizations/individuals due to personal grievances
- **Espionage** — gathering classified info for strategic advantage
- **War** — disrupting critical infrastructure or military systems during conflicts

## Attributes of Threat Actors
- **Resources/Funding:** High (nation-states, organized crime) vs. Low (script kiddies, some hacktivists)
- **Sophistication:** High (nation-states/APTs — custom malware, zero-days) vs. Low (script kiddies, some insiders)
- **Internal vs. External:** Internal (insiders, shadow IT) vs. External (nation-states, hacktivists, organized crime)

## Mitigation Strategies
- Implement **zero-trust architecture** to verify every access request
- Use **honeypots** and **honeytokens** to detect and deceive attackers
- Conduct regular **employee training** to reduce insider threats and phishing risk
- Perform **vulnerability assessments** to identify and patch weaknesses

---

