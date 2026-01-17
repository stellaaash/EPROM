Uncomplicated FireWall or UFW is a simple to use [[Firewall]], providing simple setting of rules at the host level.
# Cheatsheet
All `ufw` commands **have to be run as root**.
```sh
ufw status
ufw status numbered  # List all current rules numbered (useful for deleting rules)
ufw enable

# Create a rule to allow all outgoing connections from a Linux machine
ufw default allow outgoing

# Create allow/deny rules for a port in IPv4 and IPv6
ufw allow 22/tcp
ufw deny 22/tcp

# Delete rule number 2
ufw delete 2
```