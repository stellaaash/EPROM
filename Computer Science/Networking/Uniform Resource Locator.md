---
tags:
  - networking
---
A Uniform Resource Locator or URL is **an instruction on how to access a resource on the internet**.
# Structure
![](https://tryhackme-images.s3.amazonaws.com/user-uploads/5c549500924ec576f953d9fc/room-content/34ad66d8b90aaaa35f9536d3b152ea97.png)
`http://user:password@google.com:80/query?text=wow#french`
This totally made up URL will help us show off the different parts it is composed of:
1. **Scheme**: This instructs on what *protocol* to use for accessing the resource. This can range from [[HyperText Transfer Protocol]], [[HTTPS]] or [[File Descriptor]], for example.
2. **User**: Some services require *authentication* to log in. You can put a username and a password directly in the URL if needed.
3. **Host**: This is the [[Domain Name]] or [[IP Address]] of the server you wish to access.
4. **Port**: This is the *port* through which to access the resource.
5. **Path**: This specifies the file name or *location* of the resource on the host server.
6. **Query String**: This provides *extra information* to be sent to the requested path. For example, `/blog?id=1` would ask for the blog article with the id of 1.
7. **Fragment**: This is a reference to a location *on the actual page* requested. This can target a HTML heading, for example.