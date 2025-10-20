---
tags:
  - email
port: "110"
---
The Post Office Protocol is **designed to allow the client to communicate with a web server and retrieve email message**.
Its version 3 (POP3) is the one often used.
# How it works
## Commands
- `USER <username>` identifies the user
- `PASS <password>` provides the user’s password
- `STAT` requests the number of messages and total size
- `LIST` lists all messages and their sizes
- `RETR <message_number>` retrieves the specified message
- `DELE <message_number>` marks a message for deletion
- `QUIT` ends the POP3 session applying changes, such as deletions