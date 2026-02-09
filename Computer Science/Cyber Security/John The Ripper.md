---
tags:
---
A password-recovery utility perfect for cracking hashes.
# Single Crack Mode
While john usually uses bruteforce with a dictionary to crack stuff, it also has another mode: *single crack mode*.
This uses *word mangling* to figure out a possible password based on the username given (like if it was root, it would try root1, or root*, etc. etc.).
It can also use GECOS information found in the /etc/ files to infer information.
# Configuration
Configuration such as custom rules is put inside the `john.conf` file, usually found in `/etc/john/john.conf`.
## Custom Rules
Creating custom rules helps john to mangle keywords to find a hash's password. It's useful when you know the password requirements of your target (special characters, etc...).
You can name your custom rule using the first line `[List.Rules:NameOfRule]` so as to be able to use it as a john argument later on.
You can then use [[Regular Expression]] patterns to **define where the word will be modified**.
Jumbo John has a set list of pre-defined rules if you need detailed, working examples.
### Example
For example, to define a rule that would match the example password `Wowpassword1!` from the word `wowpassword`, you would create this:
```
[List.Rules:WowPassword]
cAz"[0-9] [!$%@]"
```
Utilises the following:
- `c`: Capitalises the first letter
- `Az`: Appends to the end of the word
- `[0-9]`: A number in the range 0-9
- `[!$%@]`: The password is followed by one of these symbols
### Resources
[Openwall Wiki](https://www.openwall.com/john/doc/RULES.shtml)
# Cheat Sheet
```bash
john [options] [file path]

# Documentation
john --list=format  # List possible formats

# Basic cracking
john --wordlist=[path to wordlist] [path to file]  # Let john the ripper figure out the hash type and crack it using the provided wordlist
john --format=[format] --wordlist=[path to wordlist] [path to file]  # If you know what the type of the hash is, provide it using --format

# Single Crack mode
john --single --format=[format] [path to file]  # Use single crack mode. You need to prepend the hash with the username and a : for john to understand what to mangle

# Custom rules
john --wordlist=[path to wordlist] --rule=WowPassword [path to file]  # Use custom rule WowPassword (see section on the matter)

# Cracking hashes from /etc/shadow - John ships with a tool called unshadow that is specialized in linux passwords: those need to be "unshadowed" before being cracked
# The results can then be used with standard john to be cracked (usually with sha512crypt).
unshadow [path to passwd] [path to shadow]  # You need to provide both /etc/passwd and /etc/shadow.

# Cracking password-protected zip/rar files
zip2john file.zip  # Extract a hash from a given zip file as to be able to crack it using john
rar2john file.rar  # Extract a hash from a given rar file as to be able to crack it using john

# Cracking SSH keys
ssh2john id_rsa.key  # Extract a hash from a private ssh key to be able to crack the password protecting it
python3 ssh2john.py id_rsa.key  # Also available a python script, usually in the john install folder
```