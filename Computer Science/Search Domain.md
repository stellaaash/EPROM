---
tags:
  - networking
---
Search domains are a [[Domain Name System]] feature that enables **automatic completion of partial domain names**.
# How it works
When you type an incomplete  such as [[Domain Name]] `ping webserver`, your system will automatically try to append the search domains to find a match.
So if you've got `company.local` setup as a search domain, the command would be completed as `ping webserver.company.local`.
# Use cases
Search domains are mostly useful in corporate networks where you have internal servers like `mail.company.com` or `fileserver.company.com`.
If you wanna have fun with a home lab though, this could be nice to keep in mind.
But for home networks, those aren't usually used.