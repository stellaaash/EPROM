A web shell is a process where **a compromised web page can be used to input commands that will run on the [[Web Server]] itself**.
Web shells can be written in several languages supported by web servers, like PHP, ASP, JSP or even simple CGI scripts.
Once the web shell is uploaded on the server, you can access it via a GET request that uses parameters in the [[Uniform Resource Locator]] to execute commands, like `http://victim.com/uploads/shell.php?cmd=whoami`.
# [Examples](https://www.r57shell.net/index.php)
Here are some freely available web shells:
- [p0wny-shell](https://github.com/flozz/p0wny-shell)
- [b374k shell](https://github.com/b374k/b374k)
- [c99 shell](https://www.r57shell.net/single.php?id=13)