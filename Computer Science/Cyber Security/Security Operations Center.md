---
tags:
---
A Security Operations Center or SOC is a **dedicated facility operated by a specialized security team**.
This team **aims to monitor an organization's network and resources and identify suspicious activity to prevent damage**.
Their main jobs is detecting and responding to incidents.
# Detecting something fishy
- **Detect vulnerabilities**: the SOC of an organization might figure out some computers of a department have a vulnerability, so they apply the patch
- **Detect unauthorized activity**: clues such as connections from other countries can help the SOC figure out some logins have been compromised
- **Detect policy violations**: violations of policy change in meaning from company to company, but they usually mean someone did something they shouldn't have like downloading pirated files or sending important files unencrypted
- **Detect intrusions**
# Responding to the fish
Once an incident has been isolated, the SOC can **respond accordingly to minimize the impact and perform a root analysis**.
# Three pillars
## People
SOC tools and automated detection utilities generate **a lot of warnings and errors**.
This is when a human team steps in to filter and isolate the important information to provide a response.
### Roles
- **SOC Analyst (Level 1)**: Anything detected by the security solution would pass through these analysts first.
  These are the first responders to any detection. SOC Level 1 Analysts perform basic alert triage to determine if a specific detection is harmful. They also report these detections through proper channels.
- **SOC Analyst (Level 2)**: While Level 1 does the first-level analysis, some detections may require deeper investigation.
  Level 2 Analysts help them dive deeper into the investigations and correlate the data from multiple data sources to perform a proper analysis.
- **SOC Analyst (Level 3)**: Level 3 Analysts are experienced professionals who proactively look for any threat indicators and support in the incident response activities.
  The critical severity detection reported by Level 1 and Level 2 Analysts are often security incidents that need detailed responses, including containment, eradication, and recovery. This is where Level 3 analysts’ experience comes in handy.
- **Security Engineer**: All analysts work on security solutions.
  These solutions need deployment and configuration. Security Engineers deploy and configure these security solutions to ensure their smooth operation.
- **Detection Engineer**: Security rules are the logic built behind security solutions to detect harmful activities.
  Level 2 and 3 Analysts often create these rules, while the SOC team can sometimes also utilize the detection engineer role independently for this responsibility.
- **SOC Manager**: The SOC Manager manages the processes the SOC team follows and provides support.
  The SOC Manager also remains in contact with the organization’s CISO (Chief Information Security Officer) to provide him with updates on the SOC team’s current security posture and efforts.
## Process
Each role in a SOC **has its own Processes** which help them carry out their jobs.
### Alert Triage
Alert Triage consists in **analyzing a given alert with the three W questions:** Who, What, Why, Where and When.
### Reporting
Harmful alerts have to be escalated to higher-level analysts for them to respond to it.
This can take the form of *tickets* that will be assigned to the relevant people.
### Incident Response and Forensics
In critical scenarios, high-level teams **initiate an incident response**.
A few times, a detailed forensics activity also needs to be performed. **This helps to isolate the root cause of the incident**.
## Technology
The technology portion of a SOC is the **tools and utilities they use to detect and respond**.
### Tool Examples
- [[Security Information and Event Management]] (SIEM)
- [[Endpoint Detection and Response]] (EDR)
- [[Firewall]]