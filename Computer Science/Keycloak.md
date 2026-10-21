---
tags:
  - tool/infra
---
Keycloak is an **identity provider that your app can refer to to authenticate its users**.
It has its own container, its own database. It's self-contained; a ready-made solution for login and registering. This way, **your own app stores no passwords, and has no login page**.
It supports many protocols, including [[OpenID]], [[OAuth 2.0]], and [[Security Assertion Markup Language]].
It provides features such as **user management, 2FA, permissions and roles, creating token services, etc.**
# How It Integrates
With your app, the usual pattern is that you **leave authentication to Keycloak, and enforce authorization yourself**. The Keycloak server might give you the user's roles, but what those roles mean is up to your application.
# Terminology
## Realm
An **isolated space with its own users, apps, and settings**.
## Clients
The **apps registered in a realm**.
## Users/Groups/Roles
**Who exists, and the labels** that will be included in the OIDC tokens **for apps to make their own decisions** on what to give access to the users based on those labels.
## Federation/Brokering
Keycloak could **read the users from an existing directory** like [[Lightweight Directory Access Protocol]] or [[Active Directory]], or even **let people login using external providers** like Microsoft or Google.
Even when working with external providers or directories, **Keycloak still issues its own tokens to your apps**.