---
tags:
  - tool
---
An event streaming platform.
Kafka has a **client-server structure through [[Transmission Control Protocol]]**.
It can be deployed basically anywhere you want or need.
# Concepts
## What is Event Streaming?
Event streaming is **capturing data from real-time source (databases, sensors, other devices, cloud services, ...) in the form of a stream of events**.
You store these for later retrieval, allowing for manipulation, processing, and reacting to them in real-time, but also asynchronously.
This streamlines the transmission of data in real-time, allowing the right applications to access the relevant data at the right time.
### Kafka's Capabilities
Kafka is an event streaming platform. This means a few things about its functionality:
1. It can **publish and subscribe** to streams of events. This means write and read to them, respectively.
2. It can **store** those streams of events for as long as you want.
3. It can **process** streams of events as they occur, or retrospectively.
## Servers
Kafka is run as **a cluster of one or more servers**, which can be in different locations.
Some of these form the **storage layer, called the *brokers***. Others **run Kafka Connect to continuously import and export data as event streams** so that Kafka can be integrated with your existing systems (databases, apps, anything you'd like).
A Kafka cluster is highly scalable and fault-tolerant. Any server can do any work, and if one of them fails, the others can take its place to ensure continuous service.
## Clients
Clients allow you to **write applications and microservices that work with event streams**.
Kafka has some of these included, but there are **many community clients that exist, including libraries for [[Go]], [[Python]], C/C++, etc.**
## Event
An event is basically **"something happened"**. Pretty broad, because that's the point: **all it is is a combination of key, value, and a time**.
## Producers
As you might guess, those are **applications that publish (write) events to Kafka**.
Producers and consumers are fully decoupled, and one doesn't need to wait for the other at any point.
## Consumers
On the other side, consumers **subscribe to (read and process) these events**.
## Topics
Topics help to **organize events**, kind of like folders in a filesystem.
Topics are multi-producer and multi-consumer: they can have any number of producers or subscribers at a given time.
**Events in a topic are not deleted after consumption**; as such, they can be consumed at any time necessary, whether in real-time or retrospectively.
Instead, you **define how long Kafka should retain your events per-topic**. Kafka doesn't degrade in performance as data size grows, so you shouldnn't have to worry about that.
## Partitions
Topics are partitioned, whcih means **they are spread over a number of *buckets* located on different Kafka brokers**.
This allows you to **distribute the placement of your data, which is very important for scalability**. This way, you allow client applications to read/write events from/to many brokers at the same time.
When a new event is published to a topic, it is **appended to one of the topic's partitions**. Events with the same key are written in the same partition, making sure that **the order of events is kept for a given topic-partition**.
### Replicating Partitions
Partitions can easily be replicated. A leader partition will be appointed, and the others will be its followers, replicating as the partition changes.
# Kafka Connect
