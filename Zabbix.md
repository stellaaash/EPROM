---
tags:
  - tool
---
**An open-source software allowing extensive monitoring of servers and clients's health and integrity.**
Greatly configurable, it can target any device on which a Zabbix agent exists.
# [Vocabulary](https://www.zabbix.com/documentation/current/en/manual/definitions)
Click the header for the official list of terms defined in the Zabbix Manual.
# Structure overview
## Server
The central component receiving reports from the agents and stocking everything in the Database.
Essentially the central repository where all configuration, statistics and operations are stored.
It is the entity that is responsible for alerting administrators and sending notifications when triggers happen.
## Database
Contains all the configuration information and the data gathered by Zabbix Agents.
Usually also on the same machine as the Zabbix server, unless is it very large, in which case it's probably a good idea to give it a discrete rig to run on.
## Web interface
An easy access to Zabbix in a web app.
Usually (but not always) part of the Zabbix Server, on the same physical machine as the Server one.
## Proxy
To collect performance and availability data on behalf of the Server.
This allows to take some load off of it and distribute it over an array of Proxies to reduce the load on a single server.
## Agent
Zabbix Agents are clients running on the target machines, tasked with collecting the relevant data and sending to it to the Server or a Proxy.
They are deployed on the monitoring targets directly, running continually in the background.
There are two types : Zabbix Agent and Zabbix Agent 2.
The first is lightweight, supported on many platforms and written in C.
The second is more flexible and extensible, written in Go.
## Data flow
Setting up a data flow in Zabbix is pretty tough, but extremely powerful.
For example, you could create something that sends you an email if the CPU load on a given server is too high:
- Create a host entry for the server
- Create an item for monitoring the CPU
- Add a trigger for when the CPU usage is too high
- The trigger is followed by an action to send you an email
# Related software
Zabbix works around modern web servers, database engines and [[PHP]].
# Structure deep dive
## Server
You usually set the server as a non-root **daemon** process (using [[systemctl]] for example). Zabbix can only run on [[Unix]] systems.
___
It has a built-in High Availability feature which, if turned on, runs multiple Zabbix Server nodes in a cluster, with only one active.
If one of them fails, another one picks up and continues where the other left off, in this way always having an instance up and running.
## Agent (1)
The Zabbix Agent is **deployed on the monitoring target** to actively check ressources and **report to the Zabbix Server** (or a Proxy, more on that below).
Same as the Server, it runs as a background process, using [[systemctl]] on unix-likes and a [[Service]] on Windows.
___
Zabbix agents use native system calls and as such are highly efficient.
### Passive vs Active checking
Passive checking occurs when the Agent **receives a specific request** from the Server (or Proxy).
For example, the Server might request some data about the CPU load, and the Agent obliges and returns the result.
___
Active checking, on the other hand, occurs when the Agent checks for data and sends it **without prior demand**.
This means it checks for the given data all the time, without being prompted by the Server or a Proxy.
It does so by retrieving a list of monitoring Items from the Server (Items are the specific things you want to monitor like CPU usage, RAM usage, etc...).
___
Passive or Active checking is **chosen when configuring the Items** (Items of type "Zabbix agent" or "Zabbix agent (active)").
## Agent 2
**A newer generation of the Zabbix Agent**, written in [[Go]] instead of [[C]].
Here are the listed enhancements:
- Reduce the number of TCP connections.
- Provide improved [concurrency of checks](https://www.zabbix.com/documentation/current/en/manual/concepts/agent2#check-concurrency).
- Be easily extendable with [plugins](https://www.zabbix.com/documentation/current/en/manual/extensions/plugins), which provide simple checks with minimal code and support complex checks consisting of long-running scripts and standalone data gathering with periodic reporting.
- Function as a replacement for Zabbix agent, supporting all previous features.
___
The Zabbix Agent 2 also **supports passive and active checking**.
It runs as a daemon on [[Unix]]-likes, but as a standalone process on [[Windows]] (though it can also be run as a [[Service]] if wanted).
## Proxy
**A process that collects data from Agents on behalf of the Server, and then sends that data to it.**
Deploying a proxy is optional, but very useful for cases where a lot of Agents have to report to the Server, potentially overwhelming with individual requests.
Ideally, only Proxies collect the data, before sending it over to the Server, thus letting the Server's load be reserved for processing and notifications.
**Zabbix Proxies require a separate database.**
## Java gateway

## Sender

## Get

## JS

## Web service

# Resources
[Zabbix Manual](https://www.zabbix.com/documentation/current/en/manual)