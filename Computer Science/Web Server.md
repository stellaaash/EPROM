---
tags:
  - networking
---
A web server is software (and the underlying hardware) that **accepts [[HyperText Transfer Protocol]] requests**, or it's secure variant [[HTTPS]], and fulfills them.
A user agent, like a web browser or crawler, starts communications by **making a request** for a specific resource hosted on the server.
That can include **web pages or any other resource** you can load using HTTP.
If configured correctly, a web server may also **accept resources and store them** for later use.
# How it works
Web servers serve the files present at their root directory. For [[Apache]] and [[nginx]], for example, this directory is by default `/var/www/html`.
So if you call for `http://example.com/picture.jpg`, the server will give you `/var/www/html/picture.jpg`.
## Virtual Hosts
Web servers **can host multiple websites with different domain name**. To achieve this, they use Virtual Hosts.
The server checks the *hostname* being requested from the HTTP headers and matches that against its virtual hosts.
In practice, virtual hosts are just text-based configuration files specifying which [[Hostname]] gets which files.
If no match is found, the default website is provided instead.
The real power of virtual hosts comes in the fact that **each virtual host can have its own root directory on the server's drive**.
This allows the hosts to display different content than the other websites present on the server.
## Static vs Dynamic content
