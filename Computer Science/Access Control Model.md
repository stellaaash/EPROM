---
tags:
  - security
  - concept
---
A system **controls access to resources** based on a given access control model.
# Discretionary Access Control - DAC
When using DAC, **the resource owner explicitely adds users with the proper permissions**.
Essentially, you add everyone that needs access to a resource manually.
This works fine for a few people, but isn't very scalable.
# Role-Based Access Control - RBAC
This ups the ante on DAC, by introducing *roles*.
**Each role has specific rights**, and instead of assigning rights to users directly, **you assign the roles themselves**.
This has many advantages, including that it's easier to manage permissions: **instead of adding individual permissions for a task, you assign the role for that task**.
# Attribute-Based Access Control - ABAC
RBAC is nice, but is pretty restrictive once your business logic has people spanning multiple roles
ABAC aims to solve this by providing a **more flexible approach: defining access based on attributes**.
For example, you could have attributes on resources dictating access at specific hours, and then attributes on a team of people, dictacting what resources that team has access to.
With this model, the sky is the limit, and **you can go as granular as you need**.
You can even combine it with RBAC for the best of both worlds.
# Mandatory Access Control - MAC
This model **prioritizes security above all else**, including ease of use.
Such system are **designed for specific purposes or to handle highly confidential data**.
As such, user friction is minimal, so security can spread its wings more.
## Examples
- [[AppArmor]]
- [[SELinux]]