---
tags: 
port: "21"
abbreviation: FTP
---
This protocol **helps transfer files from clients to servers**.
Its secure cousin, SFTP, runs over [[Secure shell]].
# Passive Mode Vs Active Mode
Active mode uses port 20 for data transfer, and port 21 for the rest (as does passive mode).
Passive mode is **useful when the client is behind a firewall**.
> [!NOTE] Research needs doing!

# Commands
- `USER`: Used to input the username
- `PASS`: Used to input the password
- `RETR`: Used to retrieve (download) a file from the FTP server to the client.
- `STOR`: Used to store (upload) a file from the client to the FTP server.