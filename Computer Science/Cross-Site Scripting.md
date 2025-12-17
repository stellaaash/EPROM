---
tags:
  - vulnerability
---
Cross-Site Scripting or XSS is **a web application vulnerability that lets you inject code into input fields that represent content displayed on the app**.
This makes the code you inject execute as the element that needs to be displayed is loaded, getting you arbitrary code execution.
# Types of XSS
There are **multiple type of cross-site scripting vulnerabilities**.
## Reflected XSS
Reflected XSS are visible immediately after the injection: **it is projected in a response**.
For example, injecting JS code in a [[Uniform Resource Locator]]'s query.
## Stored XSS
Stored XSS occurs when **a script is saved to the server and then executed for every user who views an affected page**.
For example, submitting JavaScript code in an HTTP request to update content like PUT or POST.
# Mitigating XSS
Each app is different, so not every measure might apply to your particular case.
- **Disable dangerous renders**: Instead of using `innerHTML`, use the `textContent` property instead.
  This prevents actual HTML from being injected, but rather text that is then converted to a simple HTML paragraph.
- **Make cookies inaccessible to JS**: Set session cookies with the `HttpOnly`, `Secure` and `SameSite` attributes.
- **Always sanitize user input and output, and encode them**.
  This dramatically reduces the possibilities, but is a bit like a cat-and-mouse game to know what to sanitize for. Put yourself in the shoes of an attacker!