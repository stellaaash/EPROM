A utility that **allows you to create a Socket connection between two data sources**.

# Cheatsheet
```sh
# Extra verbose (-dd) creation of a TCP listener on port 443 to listen for a reverse shell, for example
# This essentially creates a server socket for incoming connections
# The STDOUT option directs any incoming data to the standard output
socat -d -d TCP-LISTEN:443 STDOUT
```