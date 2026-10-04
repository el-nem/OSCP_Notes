# Incident Response Lifecycle

- `Incident` = a security event that hurts (or can hurt) the CIA of a system or data
- Goal = stop the damage, remove the attacker, get back to normal, and learn from it

---

# NIST SP 800-61 (4 phases)

1. `Preparation`: IR plan, team, tools, training, contact list. Done before any incident
2. `Detection and Analysis`: find the incident (alerts, logs, user reports), confirm it is real, decide how serious it is
3. `Containment, Eradication, and Recovery`
   - `Containment`: stop it from spreading (isolate the machine, block the IP, disable the account)
   - `Eradication`: remove the cause (malware, backdoor, bad account)
   - `Recovery`: restore systems and monitor them
4. `Post-Incident Activity`: lessons learned, update the plan, write the report

---

# SANS (6 steps)

1. Preparation
2. Identification
3. Containment
4. Eradication
5. Recovery
6. Lessons Learned

Same idea as NIST, just split in more steps.

---

# Important Points

- Contain first, then eradicate. If we delete the malware too early, we lose evidence and the attacker may come back
- Keep evidence safe (memory dumps, disk images, logs) and keep the `chain of custody` if it can go to court
- `Lessons learned` is the most skipped step, but it is where the company gets better
- Link to career: `Incident Responder / DFIR` role (see `Cybersecurity Career Roles`)

---
