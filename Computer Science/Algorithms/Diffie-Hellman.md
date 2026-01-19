---
tags:
  - cryptography
  - algorithm
---
Diffie-Hellman is a **key-exchange algorithm leveraging [[Public-key Cryptography]] to safely exchange a secret between two parties**.
This secret is very often a symmetric key to be used for secure communications.
# How it works
Here are the key steps:
1. Alice and Bob agree on the **public variables**: a large prime number _p_ and a generator _g_, where 0 < _g_ < _p_. These values will be disclosed publicly over the communication channel. Although insecurely small, we will choose _p_ = 29 and _g_ = 3 to simplify our calculations.
2. Each party chooses a private integer. As a numerical example, Alice chooses _a_ = 13, and Bob chooses _b_ = 15. Each of these values represents a **private key** and must not be disclosed.
3. It is time for each party to calculate their **public key** using their private key from step 2 and the agreed-upon public variables from step 1. Alice calculates _A_ = _g_ * _a_ mod _p_ = 313 mod 29 = 19 and Bob calculates _B_ = _g_ * _b_ mod _p_ = 315 mod 29 = 26. These are the public keys.
4. Alice and Bob send the keys to each other. Bob receives _A_ = _g_ * _a_ mod _p_ = 19, i.e., Alice’s public key. And Alice receives _B_ = _g_ * _b_ mod _p_ = 26, i.e., Bob’s public key. This step is called the **key exchange**.
5. Alice and Bob can finally calculate the **shared secret** using the received public key and their own private key. Alice calculates _B_ * _a_ mod _p_ = 2613 mod 29 = 10 and Bob calculates _A_  * _b_ mod _p_ = 1915 mod 29 = 10. Both calculations yield the same result, _g_ * _a_ * _b_ mod _p_ = 10, the shared secret key.