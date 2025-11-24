---
tags:
  - vulnerability
---
IDOR or Insecure Object Reference occurs when you **don't check access on direct object references in your [[Uniform Resource Locator]]s**.
For example, having a URL like `bank.com/account?id=11111` raises questions like "what happens if I just access `bank.com/account?id=22222`?".
If the answer to that question is "you just access that bank account", you've got a serious problem on your hands.