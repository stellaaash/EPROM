---
tags:
  - cryptography
---
A Hash or *hash value* is **a fixed-size string that is computed by a hash function**.
A *hash function* is **a pure function that takes input of an arbitrary size and returns an output of fixed length**.
Hashing **helps protect data integrity and keep password confidentiality**.
# Hash Functions
Hashing is different to encryption in that **it destroys the values that are being hashed**. You can't (easily) come back to a starting value from a hash.
As such, hash functions have to be computationally hard to reverse, but still pretty easy to execute so it doesn't take too long.
**Any slight change in the input should theoretically give a completely different hash.**
## Hash Collisions
Hash collisions occur when **two different input to a hashing function give the same output**.
Hashing functions are designed to keep collisions to a minimum, but these are bound to happen at some point.
It all depends on the **length of the resulting hash**: the longer the output, the more potential inputs can be stored (a 4-character output can only theoretically store 16 different hashes).
As a result of this loophole, **MD5 and SHA1 are now considered insecure** due to the ability to engineer hash collisions.
You can **add salt (a randomly generated value unique to each hash)** to mitigate collisions. This is really just random character you add to a hash and store separately to remember which parts is the hash and which is the salt.
# Usages
## Passwords
When a server keeps a password, **it doesn't keep it in plaintext**. It uses a known hashing function to hash it, then keeps the resulting hash in its database.
When a user tries to log in, it compares the stored hash with the hash of the password given by the user (the server uses the same hashing function). **If the two hashes match, then it has to be the same password** (assuming a good hashing function).
# Hashing Algorithms Examples
- [[Message-Digest 5]] or MD5
- [[Secure-Hash Algorithm]] or SHA1/SHA256/SHA512