# Common Cyberattack Types

---

| Attack | What it is | CIA principle hit |
|---|---|---|
| **Malware** | Bad software: virus, worm, trojan, spyware, rootkit | Depends on the type |
| **Ransomware** | Encrypts files and asks for money. Many groups steal data first (double extortion) | Availability (and Confidentiality) |
| **Phishing** | Fake message to steal credentials or make the user run something | Confidentiality |
| **DoS / DDoS** | Too much traffic or requests, so the service goes down | Availability |
| **Man-in-the-Middle (MITM)** | Attacker sits between two parties, reads or changes the traffic | Confidentiality, Integrity |
| **Password attacks** | Brute force, password spraying, credential stuffing | Confidentiality |
| **Social engineering** | Tricking people, not systems (pretexting, tailgating, vishing) | Mostly Confidentiality |
| **Supply chain attack** | Attack a trusted vendor or software update to reach many targets | All three |
| **Web attacks** | SQL injection, XSS, file upload, etc. (see later modules) | Depends on the attack |

---

# Key Points

- `Virus` needs a host file and a user action. `Worm` spreads by itself over the network. `Trojan` looks like a useful program but does something bad
- `Phishing` types:
    - `Spear phishing`: targets one person or a small group
    - `Whaling`: targets executives
    - `Vishing`: by phone call
    - `Smishing`: by SMS
- `Brute force` = try every password. `Password spraying` = try 1 common password on many accounts. `Credential stuffing` = use leaked username/password pairs from other breaches

**Real examples:**
- Ransomware: WannaCry (2017)
- DDoS: Mirai botnet (2016)
- Supply chain: SolarWinds (2020)

---
