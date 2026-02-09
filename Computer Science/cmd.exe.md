---
tags:
---
Here is a list of notable and important commands to use in [[cmd.exe]] and [[PowerShell]] in Windows environments.
Use the `/?` to display the help page of a command.
# Stream editing
## more/less
Allows to see content in an interactive environment. You can pipe results of commands directly to less to get a nice reader interface.
# File System
## cd
Change Directory.
## dir
List current directory's contents.
```powershell
dir

dir /a  # Displays hidden and system files
dir /s  # Displays files in the current directory and all subdirectories
```
## tree
Visually represent the current working directory and its children.
## mkdir
Make new directory.
## rmdir
Remove directory.
## type
Dumps the content of a text file.
Powerful with tools like [[Windows Commands#more/less]].
## copy
Copies files.
## move
Moves (renames) files.
## del/erase
Removes files.
# Networking
## ipconfig
Display networking information, such as [[Internet Protocol]] configuration.
Use the `/all` flag for more details.
## ping
Send an [[Internet Control Message Protocol]] request to a given host.
## tracert
Trace route to a target.
Will notify if a router on the path drops the packet because of its Time To Live reaching 0.
## nslookup
Looks up a host or domain and returns its [[IP Address]].
You can provide a nameserver after the query to use this one specifically.
```powershell
\> nslookup example.com
\> nslookup example.com 1.1.1.1
```
## netstat
Displays current network connections and listening ports.
```powershell
\> netstat

\> netstat /a  # Displays all established connections and listening ports
\> netstat /b  # Shows the program associated with each listening port and established connection
\> netstat /o  # Reveals the process ID or PID associated with the connection
\> netstat /n  # Uses a numerical form for addresses and port numbers
```
# Disk Management / File System
## chkdsk
Checks the file system and disk volumes for errors and bad sectors.
## sfc
Scans system files for corruption and repairs them if possible.
Use `/scannow` to scan now.
# Process management
## tasklist
List running processes.
```powershell
tasklist /FI "imagename eq process.exe"  # Find processes related to process.exe
```
## taskkill
Kills a process.
```powershell
taskkill /PID target_pid
```
# OS/Terminal
## set
List and set environment variables in the current terminal.
## ver
Displays the Windows version.
## systeminfo
Displays various information about the system, like CPU and memory details.
## driverquery
Displays a list of installed device drivers.