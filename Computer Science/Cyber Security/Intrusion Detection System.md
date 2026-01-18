An Intrusion Detection System or IDS is a **system looking for unauthorized access or behavior on a network**.
Upon detection of intrusion, an alert is generated and sent to the relevant staff.
# Types of IDS
An IDS can be deployed in the following ways:
## Host Intrusion Detection System
Installed **individually on the hosts**; responsible for only detecting threats associated with that host.
They provide detailed visibility of the host's activities, but can be challenging to manage in large networks with a large number of hosts, as they are typically resource-intensive.
## Network Intrusion Detection System
Useful for **detecting threats on the whole network**, regardless of specific hosts.
They monitor the network traffic to detect suspicious activity, and provide a centralized view of all alerts and detections throughout the whole network.
# Detection Modes
## Signature-Based IDS
Detects attacks **based on their signatures**, stored in a comprehensive database.
Obviously, the more furnished the database is, the more attacks will be detected before they become effective.
The main problem with Signature-Based IDSes is that **they cannot detect zero-day attacks**.
These are quick and efficient in their resource utilization. As such, they might be sufficient for small scale, non-essential systems.
## Anomaly-Based IDS
This type of IDS **learns the baseline behavior of the network or system, and detects deviation** to figure out when attacks are occurring.
This allows them to **detect zero-days**, but might also push them to **issue a lot of false-positives**, as deviations in a network's behavior are pretty common.
## Hybrid IDS
A hybrid IDS **does both signature-based detections as well as anomaly-based**, combining the strengths of both approaches.