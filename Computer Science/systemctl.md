Systemctl is a **tool used to interact with the [[Systemd]] system and service manager**.
See the Systemd page for details about terminology and the inner workings of the manager.
# Cheatsheet
```bash
# List units that systemd currently has in memory
systemctl list-units

# Display status information about the whole system
systemctl status
# Display status information for a unit
systemctl status UNIT

# Show properties of the manager itself
systemctl show
# Show properties of one or more units or jobs
systemctl show UNIT|JOB

# Show the man page for one or more units, if available
systemctl help UNIT

systemctl start UNIT
systemctl stop UNIT
systemctl reload UNIT
systemctl restart UNIT
```