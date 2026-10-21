---
tags:
  - protocol
abbreviation: OIDC
---
OpenID is a **decentralized authentication protocol** that allows users to be authenticated by co-operating sites (*relying parties*) using a third party identity provider.
It **removes the need for you to implement your own login system**, and allows users to **login to multiple websites using one unique identity**.
# OpenID Connect
OIDC is the **third generation of OpenID technology**. It is based on top of the [[OAuth 2.0]] authorization framework and [[JSON Web Tokens]].
As such, it allows **clients to verify a user's identity based on the authentication performed by an authorization server**, and also get some basic info about that user.
## The Spec
OIDC uses JWT signing, but expands upon it by establishing a few things:
- When a user logs in, the OIDC provider gives the app an *ID token*, which must be a signed JWT.
- The ID token must contain certain fields (who issued it, which user, which app it's for, when it expires).
- The app must verify it a certain way, and the provider must provide a way to access the public keys.
## What's in an ID Token
- `iss` - *issuer*: Who created the token
- `sub` - *subject*: For which user; this must be an ID that never changes.
- `aud`- *audience*: Which app this token was made for
- `exp` - *expiration*
- `iat` - *issued at*
- Optional profile info such as `email` or `name`
OIDC spec says that, for a token to be trusted, a few things must happen when you app verifies the token:
1. The jwt signature must be valid, verified using the public key
2. `iss` it the issuer your app expects and no other
3. `aud` is the app's client ID
4. `exp` is still in the future
The third check is what prevents standard attacks where you'd take a token minted from another app to your own app, and it would allow you to log in.
# Resources
- [Wikipedia - OpenID](https://en.wikipedia.org/wiki/OpenID)