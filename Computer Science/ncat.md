An improved version of [[Netcat]] distributed by the [[NMAP Project]].
**Provides encryption** alongside other features.
# Cheat Sheet
```sh
# Listen for incoming connections on port 4444
ncat -lvnp 4444
# With SSL
ncat --ssl -lvnp 4444
```