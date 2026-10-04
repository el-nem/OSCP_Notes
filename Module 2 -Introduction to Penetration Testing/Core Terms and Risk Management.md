# Core Terms and Risk Management

---

# Core Terms

- `Asset`: anything valuable to the company (data, servers, people, reputation)
- `Threat`: anything that can cause harm (attacker, malware, natural disaster)
- `Vulnerability`: a weakness in a system, process, or person (unpatched software, weak password)
- `Exploit`: code or a method that uses a vulnerability
- `Risk`: the chance that a threat uses a vulnerability and causes impact
    - Simple formula: `Risk = Likelihood × Impact`
- `Attack Surface`: all the points where an attacker can try to get in (open ports, web apps, APIs, employees)
- `Zero-day`: a vulnerability the vendor doesn't know about yet, so no patch exists
- `IoC` (Indicator of Compromise): evidence that an attack happened (bad IP, file hash, strange process)

**Example:**
- Asset = customer database
- Vulnerability = old Apache version on the web server
- Threat = attacker with a public exploit
- Risk = the attacker uses the exploit and steals the database

---

# Risk Management

**Risk assessment steps:**
1. Identify assets
2. Identify threats and vulnerabilities
3. Estimate likelihood and impact
4. Prioritize (highest risk first)

**4 ways to respond to a risk:**

| Response | Meaning | Example |
|---|---|---|
| **Mitigate** | Reduce the risk | Patch the server, add a firewall rule |
| **Accept** | Live with it (risk is low, or fix costs more than the damage) | Old test server with no sensitive data |
| **Transfer** | Give the risk to someone else | Cyber insurance, outsourcing |
| **Avoid** | Stop the activity that creates the risk | Shut down an old system nobody needs |

- `Residual Risk`: the risk that is left after we apply controls. It is never zero

---

# AAA

- `Authentication`: who are you? (password, MFA, biometrics)
- `Authorization`: what are you allowed to do? (permissions, roles)
- `Accounting`: what did you do? (logs, audit trails)

**Example:** I log in to a server with my password (authentication) → I can only read one folder (authorization) → the server logs every file I open (accounting).

---
