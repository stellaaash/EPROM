---
tags:
  - cryptography
---
PGP or Pretty Good Privacy is **software that implements encryption for files, performing digital signing ([[Certificates]]), and more.**
GnuPG or GPG is an open-source implementation of the OpenPGP standard. It is often used to protect the confidentiality of email messages.
# GPG Cheat Sheet
```bash
gpg --import backup.key  # Import new PGP key
gpg --decrypt message.gpg  # Decrypt a file using imported keys
```