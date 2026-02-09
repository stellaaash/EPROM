---
tags:
abbreviation: CSRF
---
Cross-Site Request Forgery or CSRF (also sometimes called sea-surf) is a type of attack on web applications.
Usually, it involves **using an iframe to extract sensitive information from your browser**.
# An Example
Imagine you're logged into your bank, and your browser stores the cookie.
Now, you visit `totally-legit.org`, which has a dubious, hidden iframe with a [[Uniform Resource Locator]] pointing to your bank's login page.
Not only that, this now really suspicious iframe has a command embedded in its URL, engineered to send all your saving to another account once logged in.
___
Now, I know this scenario is really unrealistic, but the principle stays the same: **using cookies against you**.
The iframe scenario is just one idea among many others, but you can see how terrifying it is to know that just visiting a website after you forgot to log out of your bank account could result in problems.
# Mitigating CSRF Attacks
Modern browsers all default to a specific value for cookies and iframes: **they don't share cookies to iframes pointing to another website**.
In practice, this means that if you put an iframe for a different website than your own, your browser will **probably not comply**.
This is a security mechanism to prevent simple CSRF attacks from happening, and happens through the `SameSite` HTTP header (see [[HyperText Transfer Protocol#HTTP Headers]].
By default, this cookie is set to `Lax`.