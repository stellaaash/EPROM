Hydra is a **brute force online password cracking program**.
It is **also available through a CLI**.
# Cheatsheet
The options we pass into Hydra **depend on which service we're attacking**.
```sh
# Example for FTP
hydra -l user -P passlist.txt ftp://127.0.0.1
# Example for SSH (with 4 threads)
hydra -l user -P passlist.txt 127.0.0.1 -t 4 ssh
# Example for web forms
# Here we are using a POST request at the root of the server and outputting verbose output
# The ^USER^ and ^PASS^ clauses will get replaced with the strings found in the passlist
hydra -l user -P passlist.txt 127.0.0.1 http-post-form "/:username=^USER^password=^PASS^:F=incorrect" -V
```