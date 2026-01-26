The Internet Protocol Security or IPsec is **a secure network protocol suite that authenticates and encrypts packest of data**.
It ensures secure, encrypted communications between two computers over an [[Internet Protocol]] network.
It is notably used in [[Virtual Private Network]]s.
# How does it work, really?
IPsec connections include a few different steps:
1. **Key exchange**: The connection starts by exchanging cryptographic keys.
   These will be useful for encrypting the devices and, after transmission, decrypting them.
2. **Packet headers and trailers**: IPsec adds several headers to data packets.
   Those headers add relevant information for authentication and encryption.
   IPsec also adds trailers, which go after each packet's payload.
3. **Authentication**: IPsec provides authentication for each packet, like a stamp of authenticity.
   This ensures the source of a packet is trustworthy.
4. **Encryption**: IPsec encrypts the payloads within each packet, as well as each packet's IP header.
   This keeps data private and secure over the wire.
5. **Transmission**: The encrypted packets are then transmitted to their destination.
   Differing from tradition [[Internet Protocol]] traffic, IPsec most often uses [[User Datagram Protocol]] instead of [[Transmission Control Protocol]].
   This allows IPsec packets to get through firewalls.
6. **Decryption**: When at the other end of the wire, the packets are then decrypted and processed by the relevant application.