Gobuster is a **tool for enumerating web directories, subdomains and virtual hosts**.
# Commands
Gobuster has multiple commands, each corresponding to a different **target to enumerate**.
This can range from web directories to amazon S3 buckets to [[Domain Name System]] subdomains.
## VHOST enumeration
While virtual host enumeration and subdomain enumeration might look like the same at first glance, they are actually different:
- DNS enumeration makes gobuster actually query DNS entries
- VHOST enumeration just appends the wordlist entries to the hostname and tries them all via HTTPS.
# Cheatsheet
```sh
gobuster [command]

# Scan directories of a website using a wordlist
gobuster dir -u some.website.com -w wordlist.txt
# Add a delay between requests
gobuster dir -u some.website.com -w wordlist.txt -d 1500ms
# Use 15 threads
gobuster dir -u some.website.com -w wordlist.txt -t 15
# Write the results to a file
gobuster dir -u some.website.com -w wordlist.txt -o out.txt

# Use debug mode to diagnose errors
gobuster dir -u some.website.com -w wordlist.txt --debug

# Scan subdomains
gobuster dns -d some.website.com -w wordlist.txt
# Show CNAME records
gobuster dns -d some.website.com -w wordlist.txt -c
# Show IPs
gobuster dns -d some.website.com -w wordlist.txt -i
# Add a DNS server to resolve subdomains with
gobuster dns -d some.website.com -w wordlist.txt -r server.dns

# Scan virtual hosts
gobuster vhost -u http://127.0.0.1 -w wordlist.txt
# Append the domain to each wordlist element (recommended, otherwise only the wordlist element will be queried as the subdomain)
gobuster vhost -u http://127.0.0.1 -w wordlist.txt --append-domain
# Use the GET method
gobuster vhost -u http://127.0.0.1 -w wordlist.txt --m GET
# Follow redirections
gobuster vhost -u http://127.0.0.1 -w wordlist.txt -r
# Use a domain if available (recommended)
gobuster vhost -u http://127.0.0.1 -w wordlist.txt --domain=website.com
# Filter unwanted false-positive (like 404 responses)
gobuster vhost -u http://127.0.0.1 -w wordlist.txt --exclude-length 250-320
```