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
A common convention is a `cgi-bin` directory at the root of the directory tree, and to treat all executable files in this directory as CGI scripts.
## Actual Use Case
A typical use case is a web form on a page that uses CGI.
A user submits the form, which triggers a `POST` HTTP request to the server.
The server then launches the CGI script in a new [[Process]], passing the form data to it.
# CGI Format
## The CGI Request
When a web server receives a request that targets a CGI script, it has to **convert that HTTP request into a CGI one**.
Usually, the request will be passed down to the script via **standard input**.
CGI Requests also have methods that the script can accept and act upon, such as `GET`, `POST` and `HEAD`.
### Request Meta-Variables
Meta-Variables are **the mechanism by which you pass data about the request to the script**.
These are case-insensitive variables, usually written in `SCREAMING_CASE`.
The specification **defines specific mechanisms by which meta-variables are to be passed to the script depending on system**. For [[UNIX]], for example, this mechanism is **environment variables**.
The specification also **defines a lot of standard meta-variables**. All extension (implementation-defined) meta variables **must be prefixed with `X_`**.
There may also be **Protocol-Specific meta-variables**, which depend on the protocol the initial request used.
For HTTP, meta-variables prefixed with `HTTP_` can be set, **reflecting the HTTP headers to the CGI script**.
Refer to [Section 4.1](https://www.rfc-editor.org/rfc/rfc3875#section-4.1) of RFC 3875 for details on every possible meta-variable.
## The CGI Response
A CGI script's job is to **generate a response** to send back to the web server.
**It has to**, it can't return 0 without pushing anything onto the standard output.
Responses **comprise of a message header and a message body**.
### Response Headers
The headers of a CGI response are either CGI-specific, or protocol-specific, like HTTP headers to be used by the web server to send the response back to the client.
For details, see [Section 6.3](https://www.rfc-editor.org/rfc/rfc3875#section-6.3) of the CGI RFC.
# Resources
[RFC 3875 [CGI 1.1]](https://www.rfc-editor.org/rfc/rfc3875)