---
tags:
---
The **most widely used exploitation framework**. Metasploit is a powerful tool that can support all stages of penetration testing, from enumeration to post-exploitation.
It has two main version: a "Pro" version that is the commercial one (with a GUI) and the open-source "Framework" version that anyone can use.
The Metasploit Framework is a set of tools that allow information gathering, scanning, exploitation, exploit development, post-exploitation and much, much more.
# Primary Components
## msfconsole
The main CLI and interface to interact with different modules of the framework.
The mfsconsole **supports most Linux commands**, acting like a transparent wrapper to a normal linux shell.
```sh
msf6> help use  # Display help for a given command

# You can use CVE numbers, exploit names or target systems to search for modules
msf6> search ms17-010  # Search the Metasploit Framework database for a module
msf6> search type:auxiliary telnet  # Search only for a type of module

msf6> use 0  # Uses the first result of the last search command
msf6> use exploit/windows/smb/ms17_010_eternalblue  # Use the EternalBlue exploit module
msf6> back  # Leave the current context

msf6> info  # Show information on the current module
msf6> info [path to module] # Show information for a given module

msf6> show [module type]  # List modules of a given type
msf6> show options  # Show options related to the current context (exploit, payload etc)

# Setting options
msf6> set RHOSTS 10.0.0.1  # Set an option for this module only
msf6> setg RHOSTS 10.0.0.1  # Set an option globally (all modules will be affected)
msf6> unset RHOSTS
msf6> unset all
msf6> unsetg RHOSTS
msf6> check  # Some modules support preliminary checks

# Run the exploit
msf6> exploit
msf6> run
msf6> run -z  # Immediately background the session once created

# Post-exploit
meterpreter> background  # Background the current session. Ctrl Z also works
msf6> sessions  # Show all current sessions
msf6> sessions -i 2  # Bring session 2 to the foreground
```
## Modules
*Modules* are small components within the Metasplit Framework that are built to **perform a specific task**, such as exploiting a vulnerability, scanning a target or brute-forcing.
### Types of modules
- Auxiliary: Supporting modules, such as scanners, crawlers, fuzzers etc...
- Encoders: Encode the exploit and payload to hide it from signature-based antiviruses.
- Evasion: Direct attempts at evading security software
- Exploits
- NOPs: No OPs. These utilities do nothing for exactly one cycle, and are often used as a buffer to achieve consistent payload sizes.
- Payloads: Code that will run on the target system.
  There are multiple types of payloads: adapters (adapts another payload to a given format or shell), singles (self-contained payloads), stagers (sets up a connection to use a staged payload) and stages (allows use of larger-sized payloads).
- Post: Modules for post-exploitation.
### Payloads vs Exploits  
While exploits leverage a vulnerability, you need a payload to actually do anything with them.
Examples can range from getting a [[Shell]], loading a malware of backdoor to the target, running a command, etc...
### Inline vs Stages Payloads
Metasploit has a subtle way to help you identify single (also called “inline”) payloads and staged payloads.
- generic/shell_reverse_tcp
- windows/x64/shell/reverse_tcp
Both are reverse Windows shells. The former is an inline (or single) payload, as indicated by the `_` between “shell” and “reverse”. While the latter is a staged payload, as indicated by the `/` between “shell” and “reverse”.
## Tools
Stand-alone tools that help with vulnerability research, assessment or penetration testing.
- msfvenom
- pattern_create
- pattern_offset
## Database
Metasploit can use a [[PostgreSQL]] database to help manage multiple targets and collect intel.
Use `msfdb init` in the shell if you have a fresh install of metasploit to initialize the database.
```sh
msf6> db_status
msf6> help  # Using the help command when connected to a db displays specific commands

# Workspaces allow you to isolate different projects
msf6> workspace  # List created workspaces
msf6> workspace -a [workspace name]  # Create a new workspace
msf6> workspace -d [workspace name]  # Delete a workspace
msf6> workspace [workspace name]  # Switch workspaces

# Having a database allows you to store enumeration results
msf6> db_nmap 10.0.0.1  # Executes nmap and stores the results

# You can then recover saved information
msf6> hosts
msf6> hosts -R  # Uses stored hosts to set the options for the current module (notably RHOSTS)
msf6> services
msf6> services -S [service name]  # Search for a given service already stored in the database
```