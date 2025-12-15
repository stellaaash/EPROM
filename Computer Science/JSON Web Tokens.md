JWTs are simple tokens that **allow you to store key-value pairs on a token that provides integrity as part of it**.
The idae it that you can generate tokens you can give your users (as cookies) while being certain they won't be able to tamper with it to try and impersonate someone else.
# Structure
A JWT is composed of **three parts**, each encoded using [[base64]]:
![](https://tryhackme-images.s3.amazonaws.com/user-uploads/5ed5961c6276df568891c3ea/room-content/11c86acaea05f98045cec5634e03e997.png)
The *header* contains metadata indicating this is a JWT, as well as the signing algorithm in use.
The *payload* contains the actual key-value pair with the data the web app wants the browser to store.
The *signature* is like a hash, taken to verify the payload's integrity.
If you change the payload in any way, **the webapp will be able that the signature doesn't match the new header, and will know the data was tampered with**.
This is possible by the webapp **holding a secret** that it uses to generate the signature: this way, the client can't reverse-engineer the signature itself to make it seem like nothing changed.