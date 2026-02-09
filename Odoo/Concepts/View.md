Views define **how to see and interact with Odoo [[Model]]s**.
They are the other half of the important pair of Models and Views. Models define what exists, and views define how to interact with that data.
Views are written in [[eXtensible Markup Language]]. They live in data files that are then loaded on the database.
# View Types
There are different kinds of views, depending on how the data is to be interacted with.
A few examples include form views for editing one record, list/tree views for browsing many, KanBan for card-based workflows, search views for filtering.
# Referencing Models
Views are linked to models in their `model` attribute.
The code of views directly references the models they want to display data from.
For example, `<field name="start_date"/>` in a view directly maps to the `start_date` field of the model linked to that view.
# View Example
`<record>` defines a record in the `ir.ui.view` model, where **all view definitions are stored**.

```xml
<record id="view_rental_order_list" model="ir.ui.view">
    <field name="name">rental.order.list</field>
    <field name="model">rental.order</field>
    <field name="arch" type="xml">
        <list>
            <field name="customer_id"/>
            <field name="start_date"/>
            <field name="state"/>
        </list>
    </field>
</record>
```