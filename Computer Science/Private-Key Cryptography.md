---
tags:
---
Private-Key Cryptography is the process of encrypting data using the same key that is going to be used for decrypting the data.
# Challenges
Since the same key is used for encrypting and decrypting, it is absolutely crucial to **keep the private key secure**. This can be a challenge, especially when there are many recipients.
Another challenge is actually sharing the key in the first place. The only somewhat secure way would be to plant it directly on both sides without a third party, but that can often prove difficult.
# Examples
- Data Encryption Standard or DES: Uses a 56-bit key, which are very easily brute-forced in today's age.
- 3DES: DES applied 3 times, which makes the key grown to 168-bits. Despite this, the effective security is 112 bits. It is now deprecated as well.
- Advance Encryption Standard or AES: Adopted as a standard in 2001, it can use keys of 128, 192 or 256 bits.
# Usages
- [[Pre-Shared Key]]