---
tags:
  - Windows
---
PowerShell is a **tool from Microsoft designed to automate tasks and manage configurations**.
It combines a command-line interface and a scripting language built on the [[.NET]] framework.
# Object-Oriented CLI
Unlike most other command-line interface, **PowerShell is object-oriented** to match the .NET framework and Windows' capabilities.
Instead of being entirely text-based like most other CLIs on the market, PowerShell cmdlets (command-lets) return objects that retain their properties and methods.
## Piping
Even piping with `|` **sends objects instead of just text content**.
# Cmd-lets
Cmd-lets are structured in a Verb-Noun structure, like `Get-Content` or `Set-Location`.
## File System
### Get-Content
Get the content of a file and display it.
```powershell
Get-Content -Path ".\path\to\file"
```
### Get-ChildItem
List all files and directories in the current location, or a specific location with the `-Path` flag.
### New-Item
Create a new file or directory (item).
```powershell
New-Item

New-Item -Path ".\new_file" -ItemType "File"
New-Item -Path ".\new_file" -ItemType "Directory"
```
### Remove-Item
Remove a file or directory (item).
### Copy-Item
Copy files and directories.
### Move-Item
Move files and directories.
### Get-FileHash
Generate a hash for a file. Helps to verify file identity and detect potential tampering.
## Network
### Get-NetIPConfiguration
Equivalent to `ipconfig`, retrieve detailed information about the system's network interfaces.
### Get-NetIPAddress
Show details for all IP addresses configured on the system, including those that aren't active at the moment.
### Get-NetTCPConnection
Display current [[Transmission Control Protocol]] connections and show local and remote endpoints.
## Object Management
### Sort-Object
Sorts objects based by property values.
```powershell
Sort-Object

Get-ChildItem -Path C:\Test | Sort-Object  # Sort a directory's contents by name
```
### Where-Object
Filter objects based on properties and return only the ones that match.
```powershell
Where-Object

Get-ChildItem | Where-Object -Property "Extension" -eq ".txt"  # ==
Get-ChildItem | Where-Object -Property "Extension" -gt ".txt"  # >
Get-ChildItem | Where-Object -Property "Extension" -ge ".txt"  # >=
Get-ChildItem | Where-Object -Property "Extension" -lt ".txt"  # <
Get-ChildItem | Where-Object -Property "Extension" -le ".txt"  # <=

Get-ChildItem | Where-Object -Property "Name" -like "ship*"
```
### Select-Object
Selects objects or object properties. Useful to **show only the details one needs**.
```powershell
Select-Object

Get-ChildItem | Select-Object Name,Length
```
## Terminal-Related
### Set-Location
Change the [[Current Working Directory]].
### Get-Command
List all available cmd-lets and functions.
```powershell
Get-Command

Get-Command -CommandType "Function"
```
### Get-Alias
List all available aliases. Most of the default ones help for transition from Unix shells (cd, cat etc).
### Get-Help
Display help for a given command.
```powershell
Get-Help

Get-Help Get-Command
Get-Help Get-Command -examples  # For examples
Get-Help Get-Command -detailed  # For more information
Get-Help Get-Command -online  # For online help
```
### Find-Module
Find modules to download. **PowerShell can be expanded with new applets by downloading them from the internet.**
```powershell
Find-Module

Find-Module -Name "PowerShell"
```
### Install-Module
Install a module.
```powershell
Install-Module

Install-Module -Name "PowerShellGet"
```
## Process Management
### Get-Process
List all currently running processes.
### Get-Service
Show information about the status of services on the machine.
## OS
### Get-ComputerInfo
Display host information such as hardware specs and BIOS details.
### Get-LocalUser
List all local user accounts on the system.
## Other
### Invoke-Command
Run a command on a local or, especially, **remote hosts**.
```powershell
Invoke-Command

Invoke-Command -FilePath C:\Scripts\test.ps1 -ComputerName SRV01  # Launch a given script on SRV01
Invoke-Command -ComputerName SRV02 -Credential Domain01\User01 -ScriptBlock { Get-Culture }  # Launch the command inside of the ScriptBlock on SRV02
```