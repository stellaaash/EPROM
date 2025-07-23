---
tags:
  - programming_concept
  - cpp
  - OOP
---
The Orthodox Canonical Form is a set of guidelines for building classes that are easy to use and simple to clean.
The idea is to always have classes that have :
- A default constructor (for default values)
- A copy constructor (for assigning a [[Class]]' values to a copy of itself)
- An assignment operator (to assign the object's values to another)
- A destructor (to clean it all up afterwards).