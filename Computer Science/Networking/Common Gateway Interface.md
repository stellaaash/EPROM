---
tags:
- protocol
abbreviation: CGI
---
The Common Gateway Interface or CGI is **an interface specification for [[Web Server]]s to execute an external program to process [[HyperText Transfer Protocol]] requests**.
Such programs are usually scripts, but compiled programs are possible, too.
# The Usual Process
## Configuration
A web server that supports CGI can be configured to **interpret a [[Uniform Resource Locator]] as a reference to a CGI script**.
A common convention is a `cgi-bin` directory at the root of the directory tree, and treat all executable files in this directory as CGI scripts.

## Actual Use Case
A typical use case is a web form on a page that uses CGI.
A user submits the form, which triggers a `POST` HTTP request to the server.
The server then launches the CGI script in a new [[Process]], passing the form data to it.
