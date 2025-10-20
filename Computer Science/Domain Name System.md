---
tags:
  - networking
port: "53"
---
The Domain Name System or DNS is the mechanism by which **[[Domain Name]]s get translated to raw [[IP Address]]es** you can directly connect to.
# How it works
## DNS Requests
Here are the steps taken when requesting a domain name:
1. The host (you) begins by **checking its local cache** to see if it already knows the domain name it's trying to access.
2. If not, a request to the *Recursive DNS Server* is made, which is usually provided by your [[Internet Service Provider]].
   This server also has a local cache of recently looked up domain names.
   If a result is found locally, it is sent back to the original request's source host.
3. If the request cannot be found locally, a journey begins to find the correct answer.
   This starts with the **internet's root DNS servers**. These act as the backbone of DNS, their job is to redirect you to the correct Top Level Domain Server, depending on your request.
   If, for example, you tried `drive.google.com`, you'd be first redirected to the `.com` TLD server.
4. The TLD server holds records to find the right server that can answer your actual request. These are called *authoritative DNS servers*.
   These are often also known as **nameservers of the domain**. There are often multiple of those for a single domain, in case one or several are down.
5. An authoritative DNS server is the server that is responsible for storing the **actual DNS records for a particular [[Domain Name]]**.
   Depending on the record type, the DNS record is then sent back to the recursive DNS server, where a local copy is cached for future use.
   Then finally, the recursive DNS server sends back the answer to the original host on the local network, who will also cache it for future reuse.
DNS records also come with a *Time To Live (TTL)* value so that they aren't cached eternally.
# Types of records
- **A record**: Maps domain to IPv4 address (google.com → 142.250.191.14)
- **AAAA record**: Maps domain to IPv6 address
- **CNAME record**: Creates an alias ([www.example.com](http://www.example.com) → example.com)
- **MX record**: Specifies mail servers for a domain
  Essentially specifies the email for the domain your are querying.
  This record also comes with a priority flag telling clients in which order to try the servers.
- **NS record**: Indicates which nameservers are authoritative for a domain
- **TXT record**: Stores text information (often used for verification)
- ...
