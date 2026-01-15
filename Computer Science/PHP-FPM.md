---
tags:
  - php
---
PHP [[FastCGI]] Process Manager is **an implementation of FastCGI for PHP designed to handle high traffic websites**.
It is advantageous in the fact that it has substantially lower memory usage as other implementations of FastCGI.
# Usage
Usually, php-fpm **sits as a server** waiting to handle requests passed by a [[Web Server]].
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