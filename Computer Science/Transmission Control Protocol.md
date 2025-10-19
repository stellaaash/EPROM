---
tags:
  - networking
  - protocol
abbreviation: TCP
---
A protocol which directly complements the [[Internet Protocol]] by providing **reliable and error-checked delivery of a stream of octets between application-running hosts**.
Those applications run on an IP network.
A connection between the sender and receiver is established through a **three-way handshake** before any relevant data is transmitted.
# The wish OSI model
TCP, like the [[OSI Model]], **provides layers** through which data is processed. See [[TCP IP Model]].
# Structure of TCP packets
Packets using TCP contain a variety of headers. The most important ones to recall are listed below.
- **Source Port**: Specifies the port that the packet has been sent from originally (usually random).
- **Destination Port**: The target port is important: it specifies which port on the target will be listening for the application that uses the packet sent.
- **Source IP**
- **Destination IP**
- **Sequence Number**: When establishing connections, the first piece of data transmitted is a random number. See below for details.
- **Acknowledgement Number**: After a piece of data has been assigned a sequence number, the number for the next piece will be the sequence number + 1. See below for details.
- **Checksum**: This creates the integrity TCP is useful for. It's essentially a hash for the value being sent: if the hash is wrong, then the value (or the hash) has been tampered with, and the packet is then corrupt.
- **Data**: This header contains the actual data.
- **Flag**: This header determines how the packet should be handled during the handshake process. See below for details.
## The Three-way Handshake
This process is the one used to **establish a connection between two devices using TCP**.
It has multiple steps, each of which involves a message:
1. `SYN`: The **synchronization** request. As the initial packet, it serves to sync two devices together as to ensure efficient communications.
2. `SYN/ACK`: The receiving device sends this packet to **acknowledge the synchronization attempt** from the client.
3. `ACK`: This packet is used at any moment in the connection to **confirm that a series of messages/packets have been successfully received**.
4. `DATA`: Once a connection is established, **actual data is sent** via `DATA` messages.
5. `FIN`: This packet is used to **close the connection properly** once it is complete.
6. `RST`: This packet **stops all communication by force**, usually indicating a problem that a `FIN` message didn't work, or something else failed.
As such, **the Three-way Handshake is a `SYN` - `SYN/ACK` - `ACK` sequence of messages**.
### Sequence/Acknowledgement Numbers
Any data being sent is given **a random number sequence** and is reconstructed using this sequence and incrementing by 1.
Both hosts communicating must agree on the same number sequence for data to be **sent in the correct order**.
Here is the process:
1. `SYN`: Client: Here's my Initial Sequence Number (ISN) to SYNchronise with (`0`).
2. `SYN/ACK`: Server: Here's my ISN to SYNchronise with (`5000`), and I ACKnowledge your initial number sequence (`0`).
3. `ACK`: Client: I ACKnowledge your ISN of `5000`, here is some data that is my ISN + 1 (`0 + 1`).
All further communications increment this ISN by 1 to **ensure that the packets are reconstructed in the right order**.
### Ending the connection with `FIN`
A three-way handshake of sorts also occurs when a TCP connection is closed (important as it holds resources on both hosts):
1. `FIN`: Client: I'm done sending data, I'd like to close the connection.
2. `FIN/ACK`: Server: Sure, I received everything so I'd also like that.
3. `ACK`: Client: Perfect, goodbye.
## TCP header flags
...
# Resources
[Wikipedia](https://en.wikipedia.org/wiki/Transmission_Control_Protocol)