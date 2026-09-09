---
tags:
  - web
  - protocol
---
The WebSockets protocol was born out of a necessity for easy two way communication where **the server can just send stuff unprompted to the client**.
This happens through a persistent connection, during which the server can broadcast any information it deems fit to the client, **without the client issuing a request first**.
# How It Works
The base idea of a WebSocket connection is that it **gets upgraded from a [[HyperText Transfer Protocol]] connection** with a *handshake*.
## URI Schemes
[[Uniform Resource Identifier]]s are defined for the WebSockets protocol, and there are two of them:
- `ws` for unencrypted connections
- `wss` for encrypted connections
For example, `wss://example.com:443/websocket/demo?foo=bar`.
## Opening Handshake
Upgrading a HTTP connection to WebSockets can happen **through HTTP/1.1, HTTP/2 or HTTP/3**.
All have different mechanisms, as the original was designed solely for HTTP/1.1.
### HTTP/1.1 Upgrade Handshake
The client starts by simply issuing a `GET` request with the `Upgrade: websocket` header.
The server will then issue a `101 Switching Protocols` if it agrees, with the same header.
Then, the WebSockets connection can start outright.
#### Client Handshake Request
```http
GET /chat HTTP/1.1
Host: example.com:8000
Upgrade: websocket
Connection: Upgrade
Sec-WebSocket-Key: dGhlIhNhbXBsZSBub26jZQ==
Sec-WebSocket-Version: 13
```
The request includes the following headers:
- `Upgrade: websocket` - indicates that the client wants to upgrade the connection to use the WebSocket protocol.
- `Connection: Upgrade` - tells proxies or other intermediaries to also upgrade the connection.
- `Sec-WebSocket-Key` - a Base64-encoded random value that helps the server prove it’s a WebSocket-capable server.
- `Sec-WebSocket-Version` - the version of the WebSocket protocol the client wishes to use.
In addition to these mandatory headers, the client might also include:
- `Sec-WebSocket-Protocol` - a list of sub-protocols that the client wishes to speak, ordered by preference.
- `Sec-WebSocket-Extensions` - a list of extensions the client wishes to use.
#### Server Handshake Response
```http
HTTP/1.1 101 Switching Protocols
Upgrade: websocket
Connection: Upgrade
Sec-WebSocket-Accept: s3pPLMBiTxaQ9kYGzzhZRbK+xOo=
```
The response includes:
- `HTTP/1.1 101 Switching Protocols` - indicates the successful upgrade from HTTP to WebSocket.
- `Upgrade: websocket` - confirms the protocol upgrade.
- `Connection: Upgrade` - indicates that the connection has been upgraded.
- `Sec-WebSocket-Accept` - a value calculated from the client’s Sec-WebSocket-Key, which helps verify that the server understood the WebSocket handshake request.
If the client requested a sub-protocol, the server includes the `Sec-WebSocket-Protocol` header with the name of the chosen sub-protocol. If the client requested extensions, the server may include the `Sec-WebSocket-Extensions` header with the extensions it has agreed to use.
## Data Framing
Once the WebSocket connection has been established, **the client and server can send WebSocket data frames in either direction**.
There are **multiple types of data frames**:
- Text frames, which contain UTF-8 encoded text data
- Binary frames, which contain, well, binary data
- Control frames, which signal protocol-level stuff, like pings, pongs, and closing frames
## Fragmenting Messages
When sending a large messages over WebSockets, the protocol is able to **fragment it into smaller data frames** to simplify sending it over.
It works like this:
1. The first frame has an opcode that indicates the message type, either text or binary.
2. All following frames have an opcode of 0, which indicate they are continuing the current data.
3. The last frame has the `FIN` bit set to 1 to indicate the end of the data.
## Control Frames
Control Frames are used by the protocol to signal connection status. They are **always unfragmented (with their `FIN` bit set to 1)**, and are at most 125 bytes.
Common control frames are listed below.
### Ping/Pong Frames
These are used for **checking that a connection is still alive**.
They are also **useful to check latency**.
When a peer receives a ping, it has to respond with a pong.
### Close Frames
Close frames are used to **signal to a peer to initiate the closing handshake**.
This is the beginning of the end for a WebSocket connection.
A close frame **may contain a status code and a reason for closing in its payload**.
- 1000: Normal closure
- 1001: Going away
- 1002: Protocol error
- 1003: Unsupported data
- 1008: Policy violation
- 1011: Internal error
## Closing Handshake
The closing handshake occurs once **either party sends a close frame**.
The peer that receives the close frame should send back one as well, after which the connection is closed.
# Resources
- [Official WebSocket Website - WebSocket Protocol](https://websocket.org/guides/websocket-protocol/)