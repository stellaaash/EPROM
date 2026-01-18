Snort is one of the most widely used [[Intrusion Detection System]]s in the world.
It uses **signature-based and anomaly-based detections** to identify threats.
It can also be used as both a **packet sniffer and packet logger**.
# Cheatsheet
```sh
# Use a PCAP files for analysis
sudo snort -q -l /var/log/snort -r file.pcap -A console -c /etc/snort/snort.conf
```
# Snort Rules
![](https://tryhackme-images.s3.amazonaws.com/user-uploads/6645aa8c024f7893371eb7ac/room-content/6645aa8c024f7893371eb7ac-1725532438800.png)
**Action**: This specifies which action to take when the rule triggers. In this case, we have the action to "alert" when the traffic matches this rule.
**Protocol**: This refers to the protocol that matches this rule. In this case, we use the protocol "ICMP" when pinging a host.
**Source IP**: This determines the IP originating from the traffic. Since we want to detect traffic from any source IP, we set this as "any".
**Source port**: This determines the port from which the traffic originates. Since we want to detect traffic from any source port, we set this as "any".
**Destination IP**: This specifies the destination IP to which the matching traffic comes; it generates the alert. In this case, we used "$HOME_NET". This is a variable, and we defined its value as our whole network’s range in Snort’s configuration file.
**Destination port**: This specifies the port the traffic would reach. Since we want to detect traffic coming to any port, we set it to "any."
Rule metadata: Every rule has some metadata. That is defined at the end of the rule in parentheses. The following are its components:
**Message (msg)**: This describes the message displayed when the subject rule triggers. The message should indicate the type of activity detected. In this case, we used "Ping Detected".
**Signature ID (sid)**: Every rule has a unique identifier that differentiates it from others. This identifier is called the signature ID (sid). In this case, we set the sid to "10001".
**Rule revision (rev)**: This sets the rule's revision number. Every time the rule is modified, its revision number is incremented, which helps in tracking changes to any rule.