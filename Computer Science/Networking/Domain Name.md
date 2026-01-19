---
tags:
  - networking
  - dns
---
A domain name is a string that identifies a realm of autonomy, authority or control.
They are often used **to identify services provided through the Internet**, like websites, email services, etc...
In general, they designate a specific network domain or an [[IP Address]], like a given computer or server.
# How it works
The [[Domain Name System]] is, as its name entails, the basis for all domain names.
**Any name or string registered in the DNS becomes a domain name.**
Domain names are organized in subordinate levels, or **subdomains**.
They are all subdomains of the root DNS domain, which doesn't have a name and is represented by a singular point `.`.
1. The first level of domain names are the **top-level domains** or TLDs.
   Those include domains such as com, info, net, edu, org, and all the country code domains (.ch, .fr, etc...)
   There are two types of TLDs: gTLD (Generic Top Level Domain) and ccTLD (Country Code Top Level Domain)
2. On the second level, there is typically reservations by end-users who want to connect local networks to the broader internet.
   That can also mean "adding" to the Internet by **creating publicly accessible ressources or running websites**.
   These domains are limited to 63 characters + the TLD, and can only use alphanumeric characters as well as hyphens `-`.
3. The third level usually serves the same role as a the second level, as a **subdomain** of that level.
In `drive.google.com.`, for example, `com.` is the TLD, `google.` is the second-level domain and `drive.` is the subdomain.
## Fully Qualified Domain Names (FQDNs)
A FQDN is a domain name that is **completely specified**, which means that it contains all the parts of its DNS hierarchy.
It traditionally ends with a singular dot `.` to denote the top-level DNS domain that doesn't have a name.
Labels in the Domain Name System **aren't case-sensitive**, but you'll most often write domain names all lowercase.
Domain lengths must be kept to **253 characters or less**.
