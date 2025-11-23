---
tags:
  - database
  - SQL
---
A fork of [[MySQL]] by its original creator after it was bought by Oracle.
It maintains high compatibility with MySQL, using the same commands and APIs.
This makes it a **very good drop-in replacement to MySQL**.
# Cheatsheet
```SQL
-- Rename a user (or change its host)
> RENAME USER 'username'@'localhost' TO 'username'@'newhost';
```

[Learn SQL in Y Minutes](https://learnxinyminutes.com/sql/)
# Installation
Install both `mariadb-server` and `mariadb-client` packages for both running the database and connecting to it.
Don't forget to **secure the installation** by running `mariadb-secure-installation` afterwards!
This will allow you to set a root password as well.
# Ressources
[MariaDB Documentation](https://mariadb.com/docs)
