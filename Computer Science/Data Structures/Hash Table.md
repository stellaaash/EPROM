---
tags:
  - data_structure
---
A **key-value pair** data structure.
Also known as a **Hash Map**.
# Accessing the data
Hash Tables store each value with a specific key, by using a [[Hash]]ing function to store each pair at a specific location.
This allows for constant-time retrieval of data, because the same function is used for putting and retrieving the data.
# Collisions
Having multiple keys resolve to the same index inside of the hash table is known as a collision.
When this happens, a single index has to store multiple values, which effectively kills part of the efficiency of value lookups in hash tables:
it now has to look through the multiple values in a single cell to find the right one.
As such, try to design hash tables to have enough cells according the the amount of data you're gonna save.
# Load Factor
The ratio of available cells and data entries actually stored is known as the load factor.
Usually, you'll want a load factor of 0.7 or so, which means that for each 7 values stored, you'll want 10 cells in your hash table.
# Resources
[Wikipedia](https://en.wikipedia.org/wiki/Hash_table)