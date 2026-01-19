---
tags:
  - networking
abbreviation: CDN
---
A Content Delivery Network is a **distributed group of servers that caches content close to end users**, in many geographical locations.
The majority of web traffic of big websites nowadays is distributed using a CDN, mainly for its caching purposes that make often-used web pages load way faster.
A properly configured CDN may also help again some attacks, such as [[Distributed Denial of Service]].

> [!INFO] CNDs vs web hosts
> It is worth noting that **CNDs aren't [[Web Server]]s: they only do caching, not hosting**.
> This helps in web page delivery performance, but won't replace your web servers and hosting.

# Benefits of CDNs
## Load times
The main benefit is obviously **load time** of websites.
Think of it a bit like sitting at a banquet. Instead of asking for the spaghetti that's at the other side of the table, and it having to go through the hands of many people, you bring a big plate of spaghetti directly in front of you, so it's easier to get your plate full. Your greed sickens me.
## Reliability and Redundancy
Having multiple servers storing a web page **distributes load** and reduces the potential for a website to be unavailable.
If one server is down, the *anycast routing* will direct the request to another server that will fulfill it.