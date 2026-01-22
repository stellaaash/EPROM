---
tags: []
port: "80"
abbreviation: HTTP
---
Hyper Text Transfer Protocol or HTTP powers the world wide web.
Exists in secure form as [[HTTPS]].
# How it works
HTTP works in a *transaction* model: **a client *requests* a resource, and a server than *responds* with that resource**.
Every HTTP message starts with a *start line* which specifies the type of message being sent.
After the headers, there's always an empty line to specify that the body is coming next.
## Making requests
You can make a simple request with a single line: `GET / HTTP/1.1`.
What happens here is essentially "GET me the resource located at the root `/` using the HTTP protocol version 1.1".
Usually though, you also send other data to query other resources.
A full request might look like this:
```http
GET / HTTP/1.1

Host: google.com
User-Agent: Mozilla/5.0 Firefox/87.0
Referer: https://google.com/

```
Here, we are asking for the same resource, but providing extra information:
- We want the website `google.com`
- We're using Firefox version 87
- We've been referred to this page by `https://google.com/`
- HTTP requests always end up with a blank line to inform the server that the request has finished.
## Responding
Here's an example response:
```http
HTTP/1.1 200 OK

Server: nginx/1.15.8
Date: Fri, 09 Apr 2021 13:34:03 GMT
Content-Type: text/html
Content-Length: 98


<html>
<head>
    <title>Google</title>
</head>
<body>
    Welcome To google.com
</body>
</html>
```
Here's what's happening here:
- Here's your request's answer using HTTP version 1.1, everything went fine
- We're using nginx version 1.15.8 on the server side
- This is the current date
- The content is gonna be [[HTML]] content
- Of size 98 bytes
And then is followed by the actual content of the resource.
## HTTP Methods
### GET Request
Used for getting information from a web server.
### POST Request
Used to submit information to the web server and potentially create new entries in a database.
Examples include submitting a form or uploading a file.
### PUT Request
Used to create a resource or update information on the server.
### DELETE Request
Used to remove information or database records on the server.
### PATCH Request
Updates **part of a resource**. Useful to make small changes without replacing the whole thing.
### HEAD Request
A GET request that **only retrieves headers**. Helpful for checking only metadata of a resource.
### OPTIONS Request
Tells you **what methods are available for a specific resource**.
### TRACE Request
A bit like the OPTIONS request, but usually used for debugging. As such, most servers disable it for security reasons.
### CONNECT Request
Used to **create a secure connection**, like for [[HTTPS]]. not that common but crucial for encrypted communications.
## HTTP Status Codes
HTTP status codes are three digit numbers indicating the result of a request.
There are 5 categories of status codes.
- **100 - Information Response**: Sent to tell the client the request has been accepted and they should send the rest of the request. Aren't really used much these days
- **200 - Success Response**: The request was successful
- **300 - Redirection Response**: You are being redirected to another resource (different webpage or website)
- **400 - Client Errors Response**: The request was wrong in some way
- **500 - Server Errors Response**: The server messed up
## HTTP Headers
Headers are additional bits of information sent to the web server when making requests.
These help the server process the request appropriately.
### Common Request Headers
- **Host**: Can be used to request a specific website when a server hosts multiple ones.
  If the host header isn't present, you'll just receive the default website.
- **User-Agent**: This specifies with what browser you're trying to connect (software and version number).
  This helps the server format the website properly, notably for HTML, CSS and JavaScript features that might only work on some browser.
- **Referer**: Indicates the [[Uniform Resource Locator]] from which the request came from.
- **Content-Length**: When sending data (for the client side, this may be a form), this specifies the length in bytes of the content being sent.
- **Accept-Encoding**: This specifies what kind of compression the client browser supports so that the data can be smaller when sent over the internet.
- **Cookie**: This is data stored on the client side that is sent to the server.
  This may contain session ids, among other things that identify you to the server.
### Common Response Headers
- **Set-Cookie**: This tells the client to store a cookie to send back to the server with each request.
  You can add the `Secure` flag to your Set-Cookie header to specify that the cookie should only be sent over [[HTTPS]].
  The `HttpOnly` flag says that cookies shouldn't be accessed via javascript, helping against XSS attacks.
- **Cache-Control**: Specifies how long to store the content of the response in the browser's cache.
- **Content-Type**: Specifies what type of data is being returned, for example HTML, CSS, JavaScript, Images, PDF, Video, etc...
  This helps the browser process the data accordingly.
- **Content-Encoding**: What method has been used to compress the data before it was sent.
### Security Headers
HTTP Security Headers **help improve the overall security of a web page by providing mitigations against common attacks** such as Cross-Site Scripting, clickjacking and others.
[This website](https://securityheaders.io/) helps to analyse the security headers of any website.
- **Content-Security-Policy**: A CSP header helps mitigate against attacks like XSS (Cross-Site Scripting), where malicious code could be hosted on a separate website or domain and injected onto the vulnerable website.
  The CSP headers **says what domains or sources are considered safe for different types of resources: scripts, stylesheets or the code of the website itself**.
- **Strict-Transport-Security**: The HSTS header ensures that **web browser will always connect over [[HTTPS]]**.
  `max-age` sets the expiryt time in seconds for this setting, `includeSubDomains` also applies it to all subdomains, and `preload` allows the website to be included in preload lists (lists that browsers use to enforce HSTS before even having their first visit to a website).
- **X-Content-Type-Options**: Can be used to tell the browser **not to guess the [[MIME]] format of a resource** and to use the `Content-Type` header instead. You usually use the `nosniff` option of this header for this very purpose.
  It can also be used for other options, look it up.
- **Referrer-Policy**: Controls the amount of information send to the destination when redirections occur, like when the user clicks a link to another website.
  You can choose among options `no-referrer`, `same-origin` (to only send if the website stays the same), `strict-origin` (to only send if the protocol stays the same) and `strict-origin-when-cross-origin`.
## Cookies
Cookies are saved when the server gives you a **Set-Cookie header** with your response.
This essentially asks your browser to save a piece of data and send it back to the server with its requests, so that the server can identify you among other users, for example.
Your browser then uses the **Cookie header** to send it back to the server in its requests.
# HTTP Messages Structure
