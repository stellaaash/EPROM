Gobuster is a **tool for enumerating web directories, subdomains and virtual hosts**.

# Commands
Gobuster has multiple commands, each corresponding to a different **target to enumerate**.
This can range from web directories to amazon S3 buckets to [[Domain Name System]] entries.
# Cheatsheet
```sh
gobuster [command]

# Scan directories of a website using a wordlist
gobuster dir -u some.website.com -w wordlist.txt
# Add a delay between requests
gobuster dir -u some.website.com -w wordlist.txt -d 1500ms
# Use 15 threads
gobuster dir -u some.website.com -w wordlist.txt -t 15
```