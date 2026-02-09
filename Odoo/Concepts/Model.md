An Odoo model is **a python class that wraps a database schema** and adds a few things:
- The schema definition, as in **what fields exists and their types**
- *Business logic* methods, as in **functions that operate on that data**
- The ORM abstraction layer, as in **code that translates between python objects and the database itself**
- Metadata, as in **instructions for Odoo on how to treat the model itself**
Essentially, a model says "**here's the data structure, and here are some low-level tools to interact with it**".
# Business Logic
Business Logic refers to **behavior dictating how to interact with data stored inside of a database**.
This could be, for example, a quotation becoming a sale order when it is confirmed, an invoice's total being computed based on its items, a policy refraining a user from validating a big order without confirmation, etc.