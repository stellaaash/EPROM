---
tags:
---
Multipurpose Internet Mail Extensions or MIME are **types determining the nature of a resources circulating over the internet.**
It was originally designed mainly for email, but is now widely used in the [[HyperText Transfer Protocol]] and its derived form.
In HTTP and friends, **it is primarily used to figure out the type of a resource being transmitted, and if the receiving party can actually process that resource correctly**.
Accordingly, [[Web Server]]s attach a MIME type to all HTTP data they send out.
That's also how web browser know which kind of renderer to use: the look at the MIME type to determine if they need to load the [[PDF]] viewer, prepare to show HTML or even an image.
All of this takes the form of the `Content-type` header in HTTP. For example:
```http
HTTP/1.0 200 OK

Content-type: text/html
Content-type: text/plain
Content-type: image/jpeg
Content-type: image/gif
Content-type: video/mp4
```