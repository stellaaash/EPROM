OWASP is a non-profit foundation focused on understanding web technologies and exploitations and providing resources and tools designed to improve the security of software applications.
# OWASP Top 10 (2021)
## 1. Broken Access Control
Accessing web pages standard users aren't supposed to access is still the most widely found vulnerabilities on web applications.
Simply put, **you bypass authorization** to access resources you aren't supposed to.
### Examples
[[Insecure Direct Object Reference]]
## 2. Cryptographic Failures
A misuse or lack of use of cryptographic algorithms for protecting sensitive information.
Those failures can occur both at rest (on disk) and on the wire.
### Examples
[[Man in The Middle Attack]]
## 3. Injection
Injections occur when an application interprets user input as commands or parameters, allowing for unwanted code execution based on user input.
### Examples
[[SQL Injection]]
[[Command Injection]]
## 4. Insecure Design
These are vulnerabilities **inherent to the application's architecture**. The design itself, not the implementation, is flawed in its logic.
These can range from shortcuts in security left behind from testing stages, to just not thinking of all possible cases.
For example, in the case of a password reset 6-digit code sent by SMS, you could try to mitigate brute-forcing by rate-limiting [[IP Address]]es, but what if multiple addresses try to crack the same code and you haven't put securities in place for multiple hosts targeting the same code?
These are tough to fix once introduced, as they often result of oversight on the part of the designers, most often before the code was even written.
The best approach is to **perform threat modelling early on in the design lifecycle**.
## 5. Security Misconfiguration
These occur when **security could have properly configured, but was not**.
These can be very varied, but examples include keeping debugging interfaces up, not enabling some crucial security features, default passwords or default accounts, and many, many more.
## 6. Vulnerable and Outdated Components
## 7. Identification and Authentication Failures
These are a range of **failures related to authentication** and making sure a user has the needed rights to access a resource.
You can mitigate those weaknesses by ensuring strong password policies to evade brute forcing, rate-limiting access to resources and log-on attempts, as well as implementing multi-factor authentication.
### Examples
- Brute force attacks
- Use of weak credentials
- Weak Session Cookies
## 8. Software and Data Integrity Failures
Integrity means **being certain that a piece of data wasn't tampered with**. It is essential to maintain important data free from unwanted or malicious modifications.
You ensure integrity in part using [[Hash]]es.