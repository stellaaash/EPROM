---
tags:
  - vulnerability
---
Command Injection occurs when **server-side code like PHP in a web app makes a call to a function that interacts with the server's console directly**.
An injection vulnerability **allows an attacker to take advantage of that call to execute arbitrary code on the server**.
Past that point, all bets are off; the attacker can do whatever he or she wants under the user they gained control of, including creating a [[Reverse Shell]].
# Exploiting
## Inline commands
If you know your remote code execution takes place in a [[bash]] shell, for example, you can take advantage of inline commands to see the results of your injections.
`echo "my username is $(whoami)"`, for example.