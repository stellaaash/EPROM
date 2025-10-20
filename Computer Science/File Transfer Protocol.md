---
tags:
port: "21"
---
This protocol **helps transfer files from clients to servers**.
Its secure cousin, SFTP, runs over [[Secure SHell]].
# How it works
## Commands
- `USER`: Used to input the username
- `PASS`: Used to input the password
- `RETR`: Used to retrieve (download) a file from the FTP server to the client.
- `STOR`: Used to store (upload) a file from the client to the FTP server.