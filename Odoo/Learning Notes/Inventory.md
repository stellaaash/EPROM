# Inventory Basics
## Inventory Basics: Receive and Store Stock
- Goods represent physical products.
- Enabling track inventory enables you to track individual units for that particular product.
- Enabling the purchase checkbox on a product will also allow you to buy it from your vendors.
- In the inventory settings, make sure you enable the storage locations feature to manage locations in `Configuration -> Locations`.
- When a purchase order is confirmed in the Purchase app, a receipt is automatically added to the Inventory app's receipts, so you can make sure that the products do arrive correctly. The linked PO will appear in the source document field and column.
- The operations tab of a receipt is what you're supposed to receive. The demand command is the order amount, and the quantity is the ones we actually received.
- If the received quantity is lower than the ones we should have had, a backorder popup will appear so that the missing items can be ordered.
- The Move smart button will show you inventory moves executed for that receipt.
- In the physical inventory list view, you can use the `Relocate` action to move a bunch of items to another location (for example, if there was a mistake made my someone).
## Inventory Basics & Outgoing Shipments
- In the Inventory settings, you'll need a few features: `Barcode Scanner` to be able to scan products as they arrive and leave. `Delivery Methods` helps you automatically printing labels for the shipping boxes. `Storage Locations` and `Multi-Step routes` help define the storage locations (duh) and the actual steps required before sending or storing a product.
- In `Configuration -> Warehouses`, you'll find the configuration for your warehouses. You'll be able to choose the steps for incoming and outgoing shipments, from 1 to 3 steps. This depends on the company, if you want to immediately store products as they arrive, or having a handover from receipts and storage, for example if you have different teams.
- In an individual product, you'll see a Barcode field. It could be typed manually, or, even better, scan it with a barcode scanner while the field is selected.
- Confirming a sales order in the Sales app creates a Pick operation in the inventory app (if you have 2-step shipping selected). A `Ready` pick operation means that we have everything in stock already.
- You can use the barcode app to make picking easier. First scan the order, which will bring up the products you need to gather, as well as their locations. Go to the location, scan it. Then, you can go to the products, scan them as you bring them in, and once you're done, it'll tell you which location to drop it off at. Then, you can validate it.
- Then, in the delivery app, you'll find pending deliveries. It'll show you if everything is ready to be shipped (available and reserved), both in the operations list and the `product availability` field of the delivery order.
- The sales order will be linked to the delivery order.
- A delivery order doesn't abstract that your company is handling delivery; it just means that products are leaving the warehouse. Shipping handlers are a separate thing.
## Basic Warehouse Setup
- There are three choices when choosing your receipt and delivery processes: 1, 2, or 3-step processes. These depend on your actual business needs, and determines how your warehouse actually works. Different warehouses can have different processes.
- In Odoo, Inventory transfers drive warehouse operations.
- Multi-step processes allow you to enhance accountability of teams, and also make locating lost products or packages easier by being able to see at which stage the delivery or receipt was at.
- One-step receipt is the simplest setup. It is Odoo's default settings. This is when the workflow is straightforward: it only tracks whether items are received and stored. One step: from incoming shipment directly to the storage location.
- Two-step receipt is useful when items are first received into an input area, before being then moved into stock. This is useful when input items need to be sorted before being stored. Or, when separate teams handle receipts and storing in actual storage.
- Three-step receipt is perfect when every incoming product needs a quality check. Received items go to the input, then the quality control, and finally stock.
- You don't have to use three-step receipt to have quality control; you can use quality control points with any process configuration (1, 2, or 3 steps) to add quality checks on the transfers you want.
- One-step delivery: products are shipped directly from stock; no intermediate step.
- Two-step delivery: move products to an output location before they are consolidated and sent to shipment. This is perfect for when you have an inventory team and a shipping team.
- Three-step delivery: pick the products from storage, pack them at a separate location (or sorting, labelling, or whatever your business does before sending), and then finally put them in the output location before being shipped.
- You don't need three-step delivery to have external shipping providers, or packages. Those are separate features.
- In the inventory application, in Settings, you'll find `Storage Locations` and `Multi-step Routes`. Those need to be enabled to be able to configure 1-2-3 step processes. Then, in `Settings -> Warehouses`, you can configure your warehouses' products for incoming and outgoing shipments.
- In effect, deciding between 1 2 and 3 step processes depends on whether the products need to move locations 1, 2 or 3 times before being shipped (or stored, in case of incoming shipments).
## Warehouses & Locations
- A location is any spot where a product can sit (staging area, shelf, fridge, etc).
- A warehouse is a full physical building, with its own physical address. Most include an inbound, storage, and outbound locations.
- In Odoo, these locations follow a clear hierarchical tree structure for its warehouse locations.
- You'll need the `Storage Locations` feature turned on.
- You can access locations in `Configuration -> Locations`.
- Internal or Transit locations are considered the stock of the business, and will be used to calculate your inventory valuation.
- There are more location types than Internal and Transit, you'll have locations for vendors, customers, and more. These are used by Odoo to represent where products come and go when they arrive in your company or leave it.
- It's a bit like accounting: some locations serve to counterpart adding or removing stock, such as production, selling, losing stock for some reasons, etc.
- Make sure the warehouse has the right address, since linked documents will use that address.
## Units of Measure
- For this, you'll need to enable the `Units of Measure & Packagings` feature.
- From this, you can access the units of measure and packagins. This is also accessible from the `Configuration` menu.
- The reference unit is what unit a UoM will be converted to, and `Contains` is how much of that reference unit for each base unit.
- Once the UoMs are setup, the conversions in your documents and inventory will all happen automatically.
- In the actual inventory products, you can set a unitin the `Sales Price` and `Cost` fields, to calculate the cost of your product. This is the unit that you have internally, whether the imperial or metric system.
- Then, in the purchase tab, it gets interesting. Suppose you have a product that has multiple suppliers, including ones overseas. Some units might be different, for example with some suppliers using yards, and others meters. If you've set up your UoMs right in the configuration, and in the purchase tab, Odoo will do the conversions automatically.
## Inventory Adjustments & Cycle Counts
- Inventory adjustments are used to correct your current stock levels, for when you get something stolen or damaged. In short, any time the reality doesn't match Odoo's counts.
- Cycle counts are regular intervals to count specific parts of your inventory more regularly than the yearly usual regulation. This way, you keep track of your stock throughout the year.
- In the Inventory settings, you'll find the `Annual Inventory Day and Month` setting, setting the date for the annual accounting counting of all of your stock.
- Cycle counts are performed on locations, so you'll need the `Storage Locations` feature for that. In the location form, you'll see the `Cyclic Counting` section for that.
- `Inventory Frequency` sets the frequency of the cyclic counting. But the actual counting won't take effect until an inventory adjustment is actually performed for products in that location.
- To launch a cyclic counting, go to `Operations -> Physical Inventory`. Select the products you want to count (grouping by location makes this easier if you want to count a location). Then, in the buttons, `Request a Count`. You can then assign, schedule, and confirm.
- The counts can then be performed on the barcode app.
- The `Relocate` action is useful for moving stock to another location, for example, if an error was made when noting where the product was stored in the first place.
- If a quantity looks correct for some products, you can use the `Set quantity on hand` action to confirm your database matches the physical world.
- When a quantity doesn't match, you can simply type the right amount in the `Counted` field.
- Finally, when you're done counting, use the `Apply All` button to finish the count. The scheduled date for items in your location with be updated to the next cycle.
## Integrate Landed Costs
> This one's pretty tricky, so might be good to brush up on it before the cert!
- When you purchase a product from a vendor, there are often additional costs than the price of the product itself, like shipping, taxes, and much more. These are called landed costs. They are used to evaluate how much you actually made of profit when selling your product; not taking those into accounts could hide losses.
- To make landed costs available in Odoo, you'll need the accounting app, and then in the inventory settings, turn on the `Landed Costs` feature. You can also define a default journal for landed costs; but by default, these are recorded in the inventory valuation.
- Next, you'll need to configure the product categories to have the right inventory valuation costing methods. AVCO is the best choice for this; it will value products based on each product unit, including the landed costs associated with them. FIFO on the other hand, it will use the cost of the first product that entered the category. For landed costs, choose AVCO, or FIFO.
- You'll also need the perpetual inventory valuation. Periodic would mean valuing your inventory manually with journal entries yourself. Unless you really need to do that, best keep the perpetual valuation.
- Finally, you can also create a product that will represent the landed costs, for example, an Import Tax product. You can set it to purchase only if it only applies to products you purchase. Also, you'll set the `Service` product, since it's nod a good you can actually store. Thinking of it this way helps: you are really buying a service, the privilege of buying something else. For the case of the import tax, you're paying for the privilege of importing something.
- Setting the `Cost` field for the product will allow you to change the cost for each order you add this symbolic product to.
- Then, in the `Purchase` tab, you'll be able to set the `Is a Landed Cost` tick. This makes it so that you can allocate the price of a landing cost to a receipt once the order has been confirmed.
- The `Default Split Method` sets how the landed cost is split for products in the receipt, either equally for all products, regardless of quantity. Otherwise, you also have by quantity (evenly across all units), current cost (according to the cost of all units), by weight, or by volume.
- In the `Accounting` tab, you make sure that the expense account is the one you wanna use for this specific landed cost.
- When you create an RFQ with a landed cost, don't worry if the cost calculation isn't exact at the time of the confirmation of the document; you can still update it once you receive the bill.
- In the draft bill, you'll have a `Create landed costs` button, which will automatically populate the new Landed Cost instance with the ones you had in your bill.
- The `Transfers` field will allow you to select a receipt to link the landed cost to. Once that's done, you can update the landed cost price, and also the account in which it will be logged if that also needs to be changed.
- The `Compute` button can then be pressed, which will populate the `Validation Adjustments` tab, updating the inventory valuation with the landed costs.
## Access Rights for Inventory Teams
- When managing a user, you can set the roles for the inventory rights.
- Not that complicated, managers can have admin access to their app, and operators only have some user access. Of course, always remove the permissions from the other app if they shouldn't have access.
## Make-to-Order (MTO)
- With MTO, Odoo waits before there's actual demand before replenishing a product. This is useful for products that are tough to store, for example.
- In the inventory settings, you'll need the `Multi-Step Routes` feature enabled to have an MTO process. Also enable the `Replenish on Order (MTO)` feature. 
- Then, in a product you want to set MTO to, go to the `Inventory` tab, and `Routes`, enable `Replenish on Order (MTO)`. This isn't enough for MTO to work though, you'll need the `Buy` route set up for the automatic replenishment to work. Or, alternatively if you manufacture this product, `Manufacture`. To make those latter routes work, make sure the manufacturing or purchase information is set correctly in the right tab.
- Then, when you confirm a quotation for those products, Odoo will trigger the routes you set up with MTO. You can use the `Replenishment` smart button to go to the RFQ that Odoo created. You'll then confirm it to create a purchase order, receive it, validate it, and you're good to sell those products with the sales order.
# Replenishment
## Reordering Rules
- 