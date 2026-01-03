---
tags:
  - SQL
---
When an input in a web app is badly sanitized and you know that it queries the database (like for a login form), it might be vulnerable to SQL injection.
The process is pretty simple: you inject some SQL code inside of your form answer (the password, for example) in order to run code on the [[Database]].
# Examples
## Simple password query
For example, if you know that the password query of a login form looks like this when sent with the user `John` and a password `abc`:
```sql
SELECT * FROM users WHERE username = 'John' AND password = 'abc'
```
You can infer that if we used a single `'` inside of the password, we might be able to execute arbitrary code, like so, with the password `' OR 1=1;-- -`:
```sql
SELECT * FROM users WHERE username = 'John' AND password = 'abc' OR 1=1;-- -';
```
# Tools
There are tools available to **carry out automated SQL injections**:
- [[SQLMap]]