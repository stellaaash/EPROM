---
tags:
---
PHP [[FastCGI]] Process Manager is **an implementation of FastCGI for PHP designed to handle high traffic websites**.
**It daemonizes PHP**, which makes it run in the background instead of as a foreground process.
It is advantageous in the fact that it has substantially lower memory usage as other implementations of FastCGI.
# Inner workings of a page generator
## Pools
PHP-FPM maintains so-called **pools of processes** that are available for processing requests passed to it.
Multiple pools can exist, with different limits on how many processes there can be, and for serving different content.
Each pool has a *master process* that then **manages the pool** of *worker processes*.
If a pool doesn't have any more free processes, the master process can spawn a new one (until the limit defined in the configuration).
As for worker processes, **they just execute their designated php script and send the content back to the web server**.
After a while, the master process can **recycle worker processes**, helping to mitigate leaks and performance issues by renewing the pool as more requests are made.
When you first install PHP-FPM, there's a default pool whose config file is called `www.conf`.
# Usage
Usually, php-fpm **sits as a server** waiting to handle requests passed by a [[Web Server]].
The web server sends those requests through a [[FastCGI]] interface.
It then generates contents based on the request and sends it back to the server for further processing and sending.
## Configuration
Configuration files for php-fpm are stored in `/etc/php/X.X/fpm/pool.d`.
Each are structured in key-value pairs, here is an example of such a file for a [[Wordpress]] installation:
```php
[wordpress]
listen = 9000
listen.owner = www.data
listen.group = www.data
pm = dynamic
pm.max_children = 75
pm.start_servers = 10
pm.min_spare_servers = 5
pm.max_spare_servers = 20
pm.process_idle_timeout = 10s
```