---
tags:
  - networking
port: "80"
---
Hyper Text Transfer Protocol or HTTP powers the world wide web.
Exists in secure form as [[HTTPS]].
# How it works
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
## HTTP Status Codes
HTTP status codes are three digit numbers indicating the result of a request.
There are 5 categories of status codes.
- **100 - Information Response**: Sent to tell the client the request has been accepted and they should send the rest of the request. Aren't really used much these days
- **200 - Success**: The request was successful
- **300 - Redirection**: You are being redirected to another resource (different webpage or website)
- **400 - Client Errors**: The request was wrong in some way
- **500 - Server Errors**: The server messed up
## HTTP Headers
Headers are additional bits of information sent to the web server when making requests.
These help the server process the request appropriately.
### Common Request Headers
- **Host**: Can be used to request a specific website when a server hosts multiple ones.
  If the host header isn't present, you'll just receive the default website.
- **User-Agent**: This specifies with what browser you're trying to connect (software and version number).
  This helps the server format the website properly, notably for HTML, CSS and JavaScript features that might only work on some browser.
- **Content-Length**: When sending data (for the client side, this may be a form), this specifies the length in bytes of the content being sent.
- **Accept-Encoding**: This specifies what kind of compression the client browser supports so that the data can be smaller when sent over the internet.
- **Cookie**: This is data stored on the client side that is sent to the server.
  This may contain session ids, among other things that identify you to the server.
### Common Response Headers
- **Set-Cookie**: This tells the client to store a cookie to send back to the server with each request.
- **Cache-Control**: Specifies how long to store the content of the response in the browser's cache.
- **Content-Type**: Specifies what type of data is being returned, for example HTML, CSS, JavaScript, Images, PDF, Video, etc...
  This helps the browser process the data accordingly.
- **Content-Encoding**: What method has been used to compress the data before it was sent.
## Cookies
Cookies are saved when the server gives you a **Set-Cookie header** with your response.
This essentially asks your browser to save a piece of data and send it back to the server with its requests, so that the server can identify you among other users, for example.
Your browser then uses the **Cookie header** to send it back to the server in its requests.