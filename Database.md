---
tags:
  - database
---
Databases are **an organized collection of structured data that is easily accessible, manipulated or analyzed**.
# Types of Databases
Depending on what data will be stored, different types of databases will be more suitable.
## Relational Databases
These store **structure data**, meaning the data inserted into this databases follows a given structure.
For example, storing users could consist of `first_name`, `last_name`, a phone number, email address, password, etc...
This structured data is stored in rows and columns in a table, where each column has a data type that it is going to store.
**Relationships can then be made between two or more tables.**
### Primary and Foreign Keys
Primary keys ensure that the data contained in a certain column is unique. They identify each column by a number.
Foreign keys allow to **create the actual relationships** with other tables. **It directly refers to a primary key of another table.**
### Use cases
Relational databases are perfect for **data that is going to be stored in the same format reliably, where accuracy is important**.
A good example would be users of a service.
## Non-Relational Databases
These store data in a **non-tabular format**. This can range from key-value pairs to arrays to hash tables.
### Use cases
Non-Relational Databases are well-suited for data that can vary greately in its format.
A good example of this is user-generated content of social media.
# DataBase Management Systems
DBMS are systems that serve as **interfaces betwen the end user and the database.**
It allows you to retrieve, update and manage the data being stored.
## Examples of DBMS
- [[MySQL]]
- [[MongoDB]]
- [[Oracle Database]]
- [[MariaDB]]