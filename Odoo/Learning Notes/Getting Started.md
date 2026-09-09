> Notes for Odoo Learn's Getting Started course. Started in August 2026.
# Getting Started
## Create an Odoo Database
- The country of your database is crucial, it will be used to determine the chart of accounts and other crucial information, and since the former can't be easily changed, it needs to be correct.
- The password can be reset by admins for other users. It sends them an email to reset their password.
- Pricing for Odoo licenses is per user.
- Demo data is available from developer  mode. It will load dummy data to try and
## Navigate in Odoo
- Shortcuts are always available on the profile menu in the top right.
## Google Calendar Sync
- The Odoo Calendar app is integrated with basically every other app that features dates, like CRM, appraisals, sales, etc.
- Before doing the setup, test with a test database and test email address. This prevents potentially creating events inviting dozens of people to a meeting that doesn't exist.
- The setup uses the Google API.
	1. Start by creating a new project in Google Cloud.
	2. Select "Enable APIs & Services", and search for the Google Calendar API
	3. Enable it
	4. Go to OAuth consent screen
	5. Fill in the information, such as the support email, and the audience
	6. Create the OAuth
	7. Go to the branding page, and add your database's domain to the authorized domains
	8. In the audience page, add the google users that will be syncing their calendars
	9. Then, in the Clients page, you'll need to create a new OAuth client, with type Web application. This will be the Odoo database itself. Put in the URL of your database itself for the JavaScript origins and authorized redirect URIs (for the latter, append `/google_account/authentication`).
	10. Copy the client ID and the client secret for later.
	11. In the Audience tab, use the Publish App button to push it to production.
	12. On Odoo, go to the Calendar Settings. Turn on Google Calendar, and input the client ID and secret.
	13. Now, in the Calendar app, you'll see a new "Synchronize with Google" button. Select your account after clicking on it, and you're good to go.
- There is a button to pause the synchronization in the settings, which is a good way to pause it without deleting any credentials on either side.
## Outlook Calendar
- The setup uses the Microsoft API.
	1. On the Odoo side, go to Settings. In Calendar, enable the Outlook Calendar feature.
	2. Once it reloads, client ID and secret fields appear.
	3. A Microsoft Azure account or developer's account is needed to create a new azure app.
	   In the Microsoft Azure Portal, go to App registrations, and register a new one.
	4. Name it, and select "account in any organizational directory and personal Microsoft accounts".
	5. Set the redirect URI to the Odoo database's URI, appended with `/microsoft_account/authentication`. Same structure as for Google.
	6. Copy the application client ID and put it in the Odoo settings page.
	7. Go to "Manage", and then "Certificates & secrets". Create a new secret. Copy the secret value over as well.
	8. Use the synchronize with Outlook button in the calendar account. Use the Microsoft account you want.
## Filters and Views
- Set a default filter by hitting "Save current search" and setting it as the Default filter.
- Custom filters allow you to filter for any fields of a model, compared to a value using boolean equations.
- The Kanban view allows you to focus on a particular field of a model, by visual columns. Moving a record from one column to the other will change the value of that field to the column's value.
- The activity view displays scheduled activities for records and activity types. Red activities are overdue, yellow is for today, green for later.
## Multi-Company Basics
- You can manage multiple companies in a single database, which simplifies inter-company transactions greatly.
- Multi-Company is used for separate legal entities. Branches don't apply here.
- Creating companies is irreversible, so be very sure about what you need to do, and that your company is actually a distinct legal entity.
- A good example would be franchises, where some people don't need to access to all info, but leadership still needs access to info from all individual business.
- Branches are a good solution for divisions in a single company. They are NOT for distinct legal entities, as they submit tax records as a single legal entity.
- You can manage and create companies in the settings app.
- Make sure the country for the new company is correct, since it determines accounting and tax stuff, mainly the chart of accounts and the tax currency.
- When switching companies, having multiple checked gives you access to the records of all checked companies. The highlighted company, on the other hand, indicates the active company. All configuration changes apply to the active company, not the others, even if you checked them all.
- The fiscal localization setting in the accounting settings is crucial. It disappears after posting your first transaction, so make sure to set it correctly as soon as you create a new company.
- Changing the fiscal localization overwrites any custom chart of accounts.
- Each user has a list of allowed companies they can access records from.
- Each record has a company field. It being empty means that all companies have access to the record.
## Multi-Company Transactions

> [!QUESTION]
> I'm really not sure about understanding this video. It feels like they're talking about a demo for sales, but I'm not sure how I would adapt this to other situations.
> Some concepts are still useful, but it'd be worth revisiting multi-company transactions with the Odoo docs when I need to do some.

- Having a multi-company setup in Odoo allows you to streamline inter-company transactions.
  For example, creating a purchase order on one side will create a matching quotation on the other company automatically. Same thing for invoices, creating matching bills.
### Buyer Company Side
- In the general settings, enable the inter-company transactions feature. Make sure "Create as" is set to OdooBot. This creates the matching records with the system user, allowing you to keep track of which way the transaction occurred (the record with the real person as the creator is the origin).
- You can enable individual generation of records based on the business case. For example, enabling bill creation for invoices, or request for quotation creation for quotes.
- When testing your multi-company transactions process, go through the steps in order: start by creating the quote or invoice, and then create the fiscal layer documents on the other side (RFQ or bill). The other way around isn't so easy, back-creating a quote for an RFQ or an invoice for a confirmed bill.
- Use the dedicated inter-company purchases journal. Leave the currency field blank for maximum flexibility when multiple currencies are expected, for example for companies that operate in different countries.
- Set the supplier currency in the contact of the seller company.
- On the products that we're going to buy, set them to have no company so everyone sees them, and also set the seller and prices.
### Seller Company Side
- On the seller side, enable "Create Sales Order" to enable creating orders when the buyer confirms a purchase order.
- The Use warehouse field determines which warehouse we deliver from.
- Set the pricelists for the right currencies of the buyer company, in its contact.
- Be careful. Creating and confirming a bill on the buyer's side will never automatically create an invoice on the seller side. Always create the invoice on the seller side first, which creates the bill on the other side.
## In-App Services
- Odoo has in-app purchases to enable new services and third-parties.
- IAP Services include Document Digitization for AI transcribing documents, partner autocomplete which fetches company data from the internet to complete contact records, SMS, Lead Generation from user criteria, snail mail sends invoices by post. There are more.
- The catalogue can be found on `iap.odoo.com`.
- They don't need much configuration to work, they just work. No new app is created, they just add new features to existing applications.
- In-app purchases really just mean "buying credits". Each IAP service has its own credit.
  The cost per service varies.
- Odoo will prompt to buy more credits when running low.
- You can set an IAP account per company, using the Company field in the IAP account record.
# Using Odoo
## Odoo Calendar
- You can schedule meetings directly from a record's Chatter, by creating an activity and choosing the Meeting type. This leads us to the calendar app to choose a data and time.
- To check the availability of someone when planning a meeting, you can add the user to the attendees to display her calendar.
- Add attendees to the actual event to notify people and add the meeting to their calendars if they're Odoo users.
- You can create video calls using Odoo Discuss, directly on a meeting's record, under "Video Link".
- You can set reminders to send emails or notifications to attendees before an event. You can create your own reminder types.
- Over the attendees field in the meeting record, you can use the right button to send an email or SMS to notify the attendees.
## Schedule Activities
- Activities are basically a todo list for each record on an Odoo database.
- Green activites are for the future, yellow is for today, and red is overdue.
- The icon of the activity determines the type of the activity. It could be a call, an email, or a meeting, etc.
- The clock icon in the top right of all views lists all activities due today or in the past. It leads to the activity dashboard.
- You can create custom activity types if the default ones don't suit your needs. In the Discuss section of the settings, you can go to the Activity Types list, where you can view and manage the activity types.
- Each activity type can define what's the "next activity" in the chain of business logic. Like, after a discovery call, sending a quotation, or setting a meeting.
## Contacts - Basics
- Contacts are deeply integrated with the other apps. Getting a new CRM opportunity, or creating a new employee, or having a new sales partner? All of those are a new contact, even if the contacts app itself isn't installed yet.
- From a contact page, you can create related contacts directly. It could be useful to create a secondary contact if the address for invoicing/shipping/other is different than the main address.
- Creating a new contact and inputting a company name automatically creates the company contact, if not present yet in the database.
## Contacts - Views & More
- There's a map view for contacts, allowing you to see all clients on an interactive map.
- There's a hierarchy view for company structures of contacts.
- You can merge contacts, to quickly remove duplicates while keeping both records' information. Always double check that the destination contact is the one you want to keep.
- What you see in the contacts depends on many things, including your level of database access, and other apps installed (more smart buttons and tabs).
## Importing and Exporting Data
- Use the "I want to update data" field to make the exported file import-compatible. this is for when you want to make quick edits in a spreadsheet, before re-importing the updated data.
- You can delete, rearrange, and add fields as necessary.
- When importing, you can manually change which field is used for each column in the spreadsheet.
- Always test your import before importing truly!
## Chatter Basics
- The chatter is available on basically all records. It logs record updates, log notes, and messages sent.
- Followers are people that will be notified of activity on the record. You can set individual notification preferences.
- Log notes are internal to the company, and are never sent to the associated contact of the record. Perfect for messages to other team members. Notes also issue notifications to followers of the record's chatter.
- Sending messages sends a message directly to the associated contact. It is then kept in the chatter, so you can see the flow of conversation.
## Canned Responses
- Canned Responses are useful for pre-written messages that you can insert to save time and improve your team's communication consistency.
- They are managed in the Discuss app's configuration.
- Shortcuts are prefixed with `::`.
- Authorized groups allow you to share your canned responses with others. If that field is empty, the canned response will be visible only by you. Even admins can't access others' canned responses, unless their team is part of the authorized groups.
- Canned responses are available in all chatters, live chat, and whastapp messages, not just the Discuss app.
## Digest Emails
- Digest emails are useful for sending regular reports to team members, showing relevant KPIs and information, without overwhelming them with notifications.
- Enable the Digest Email feature in the settings to use those.
- You can configure the digest emails in the same setting in the Settings app.
- Each digest email can have its own KPIs and recipients list.
- The list of KPIs depends on the apps installed on your database.
- You can create your own metrics for KPIs with Odoo Studio.
## Custom KPIs for Digest Emails
- You'll need developer mode to add custom KPIs using Odoo Studio.
	1. In "Configure Digest Emails" in the Settings, choose your email digest.
	2. In Studio mode, add a new checkbox. Set its label, and set the technical name to start with `kpi_`. Copy the technical name.
	3. In technical settings, go to `Database Structure -> Models`. Go to the `digest.digest` model.
	4. At the very bottom of the list of fields, you will see the new checkbox boolean. Click into it.
	5. Add a new field with the same name as the boolean, with `_value` appended to it. It's a convention to bridge the connection between the new fields. This field will be your computed KPI value.
	6. Set the field type to `integer`. Set the field label accordingly.
	7. Set the base properties for the field, depending on the KPI you're going to do.
	8. Set the dependencies for the field: the boolean checkbox, and `company_id`. Separate the two with a single comma, no spaces. The dependencies will depend on the code you'll set for the field; check the docs for more info on that.
	9. It's time for the code to set your computed field. Set it accordingly to what KPI you want to compute.
	10. Back in the digest email, you can now turn on the checkbox for your custom KPI, and the computed value will be used in your digest email.
## Group Access Rights
- Group Access Rights sets access rights per- group. Wow. It's almost like it's named well.
- Groups rename effective even when users in that group change. They simplify permissions management for multiple users.
- You can change group access rights with developer mode, in `Users & Companies -> Groups`.  You can set the application the rights apply to, set the users that this applies to, and all of their rights, down to the individual menus. You can set it for menus, or even submenus, views, etc.
- In the Access Rights tab, you can set the actual read/write/create/delete access rights for each model.

# Odoo Discuss
## Odoo Discuss - Direct Messages
- The chat icon in the top right shows all conversations. You can manage your direct messages there, and create new conversations on the fly.
- Discuss is amazing to reduce distractions, since the chat panel allows you to just stay on the same view as you were.
- You can even record voice messages!
- The actual Discuss app acts as the hub for all internal communications in Odoo.
- If you have the Live Chat app installed, you'll also see the conversations in the Discuss app list.
- Unpinning a conversation in the Discuss app doesn't delete it, it just hides it until you add it again.
- Use the History tab in the discuss app to see all updates to your followed records.
## Odoo Discuss - Voice and Video Calls
- In a private conversation with someone, you can invite more people to create a group chat.
- In any conversation, you can just click "Open in Discuss" to go to the Discuss app.
- You can add descriptions to chats.
- You can generate public links to a chat to easily invite people outside your company. As soon as they open that link, they have to type in their name, and they just have access to the chat. They don't even need to be an Odoo user on your database!
- You can raise your hand during an audio/video call.
- You can click the camera icon to turn any call into a video call. You can blur your background.
- You can still send messages to the conversation during the call.
## Odoo Discuss - Channels
- Channels are just like slack/discord channels. That's it.
- That's not it.
- You need to join individual channels to see them in your discuss app. You can also leave them whenever you don't need one anymore.
- Typing a channel name in the channel list will either ask you to create a new one, or show you any existing ones.
- You can add descriptions to channels.
- You can create a link to channel to invite people, or just invite them directly.
- In the channel settings, in the privacy tab, you can define who can see and join the channel. You can set the authorized group(s), which allows you to define who can access the channel. If it's blank, anyone with the invitation link can join the channel, even external people. "Internal User" limits the channel to all internal users of the database.
- You can set an "Auto Subscribe Departments" to add employee groups, automatically adding all users that have an employee record linked to that group.
## WhatsApp Basics
- Odoo provides a WhatsApp integration for businesses that use it to talk to their customers and partners.
- It works with all Chatters.
- You'll need the WhatsApp module installed.
- You will need to set up an API connection between Meta and your Odoo database. Look at the lesson below, or check out the Odoo Docs.
- You'll need to submit WhatsApp templates to Meta for them to approve. They will be used to send messages through your database. Templates are preconfigured skeletons that get populated with the record data when you use them to send a message. It could be a customer name, or a sales order number, etc.
- Odoo provides a few preconfigured templates where relevant, but you'll definitely add and modify your own.
- The WhatsApp module has a view to configure the templates.
- You can use the appropriate button on a template to submit it to Meta. This might take awhile (hours to a day), and once done, you'll receive an email telling you that you can use that template now.
- In the WhatsApp account in the app, you can click the Sync Templates button to check for newly approved templates. This will switch existing templates to the Approved status, if they were approved.
- When you're on a contact, with WhatsApp installed, you can either send an SMS, email, or a WhatsApp message. Clicking the latter will open a choice of template, and allow you to change the template variables before sending the message.
- If a customer replies to a message sent over WhatsApp, you'll get a conversation in the Discuss app. There, you can also directly send messages without templates.
## WhatsApp - Advanced Setup
- Look at the docs for the official reference on how to link your meta developer console app and your Odoo database.
- You can set per-account user notification, in the "Notify Users" control field of the account.
- If a template has been sent more than 15 days before, the database will send a notification to all users in the field when the customer answers. If we receive an answer before 15 days of time, then only the user that sent the most recent template will be notified.
- Each team in a company could have a WhatsApp account depending on their needs.
- To configure your own templates, go to the Templates menu in the WhatsApp app.
- The "Applies to" field points to the model that the template will be used for. It's important, because each template has different dynamic fields or variables, and no two models are alike in what info you'll want to send to your customers. Think of confirmed orders or posted invoices.
- The "Phone Field" should be set to "phone" or "mobile". The number has to be a WhatsApp number. This will be the number the template will be sent to, so be careful to set the right field!
- A blank users field will allow everyone on the database to use the template.
- Header type has a few options, between image, text, location, etc. This is what will appear as the header of a message.
- You can also set the footer!
- You'll write the body by using `{{x}}` for dynamic placeholders, where `x` is the number of your variable. Your variables depend on the model the template is linked to with the "Applies to" field.
- Variables can have multiple types, username, field of model, etc. All types can be used to set specific values by the sender, while Field of model references a value from the linked model record directly.
- Portal Link is also a field type, which gives the customer a link to the record in your company's portal. 
- You can even add buttons to your template, including a quick reply, a number to call, or a link to visit your website (those are the three types of buttons).
# Business Flows
## Business Flows - Furniture Store
### Marketing - Building a Website
- There are multiple available themes for a website that you can change from the website editor's Theme tab.
- In the customize tab of the website editor, down in the Inline Text section, use the AI button to suggest alternatives to existing text. It's a useful Copywriter.
- Odoo provides a database of royalty-free images to use for your website.
- In a text field, you can type a slash command to use ChatGPT to create a paragraph.
- When building a form, you can change the action that the submit button will do. You can make it so that it creates a CRM opportunity, or do something else entirely. It all happens in the Customize tab of the website builder.
- You can even change the type of a form field, so it sets tags for the CRM opportunity, for example! It's that powerful.
### Sales - Managing the Lead
- You can actually translate messages in the chatter if you set this up correctly in your Odoo database.
- You can set the expected revenue for any lead based on the customer's answers on the form.
- Using the smart button at the top, you can see which pages the customer went through, to tailor your conversations with them.
- From the opportunity, contact the customer directly using Whatsapp or any other means you'd like, depending on what the customer provided in the online form.
- Once the customer accepts calling, you can create a new Meeting activity to note it down.
- From an opportunity, once a customer wants to buy stuff and told you what they want, you can directly create a quotation. In the quotation, as you add sales item, it'll show you the current stock availability.
- Even if an item isn't in stock, you can still send the quotation. Once the sales order is created, the procurement team will need to replenish stock in the Inventory app.
- After the sales order is created, the job of the sales team is done.
### Inventory - Replenishing Stock
- If the quotation is for stuff we don't have in stock yet, you can use the inventory app to replenish missing items. The replenishment view will show you all items to reorder by default.
- From there, you can directly order new items, and it will create a purchase order.
- You can also automate orders for items that sell often. Set the minimum and maximum stock we want. Then, click the automate button so that Odoo generates a request for quotation every time the number in stock falls below your minimum.
### Purchase - Purchasing Stock
- In the purchase application, the Request for Quotation will have arrived if we were missing some items, depending on whether we automated it, or manually created an order.
- From a request for quotation, you can see the expected delivery date for your required products, and the percentage of on-time delivery by that vendor.
- Make you have the "ask confirmation" check box ticked, so you can be sure that your products will arrive on time before the order to your own customer is due.
### Inventory - Receiving Products
- It's easier to use the Barcode Scanner feature to manage inventory. Make sure that and the Show Quantity to Count features are both enabled in the Inventory Settings.
- To configure barcodes, you can go to the individual products, and set the barcode field. This will generate the barcode automatically. If the item came in with its own barcode, you can scan it with your scanner to fill the field in with the results.
- In the warehouse, when the products have arrived, you can use the barcode application to select the order from your supplier. You can then just scan the incoming products to make sure everything has arrived correctly!
### Accounting - Paying the Bills
- Once the order has been received successfully, it's time to pay the bills.
- From the purchase order, you can create a draft vendor bill. The bill will be filled with the products and other relevant information automatically.
- Then, register a payment using the Pay button. The bill will switch to "In Payment". It's up to the accounting team then to reconcile this payment when the bank statement arrives for the current month.
### Inventory - Delivering the Goods
- Once the bill has been paid, the products are ready to be sent to our customer.
- In the dashboard, the order will be switched to "Ready", so you can see that the products are ready and you can send them directly. This is when the Product Availability shows "Available".
- You can then validate the order, and it will send a communication to the customer that their order has been shipped. The inventory team can then move forward with the shipping.
### Accounting - Sending Our Invoice
- The order has been shipped. Great! Now it's time for the customer to pay their dues.
- From the sales order in the quotations, you can create an invoice using the appropriate button directly. Alternatively, you can create invoices in batches for all the current completed order. This happens in the "To Invoice" tab in the Sales app.
- From there, you can check the quotations to create invoices. Then, create drafts.
- Now, you just need to send them out to the customers. This could happen in the Accounting application as well.
- In the latter, you can directly send the invoice in the actions, with a WhatsApp message.
- Once the customer's payment has been received, you can select "Pay" to create a payment for the invoice. Same thing as the bill, this payment will have to be reconciled with your bank statement later on.
### Configuring Products
- For products, you'll need to configure vendors on the products for RFQs to be created automatically.
- Also set the delivery time for your vendors so you can go with different vendors depending on the speed your order needs.
- Weight and volume info are needed for shipping volumes.
## Business Flow - Events & Marketing
### Events - Creating and Managing Events
- Event tracks are for example talks and happenings that will occur during an event.
- Events can have sponsors and rooms, as well.
- Rooms are virtual spaces where attendees can talk with experts about a specific topic. You can set a topic, an audience, and a max capacity, as well as a language for it.
- The room can then be published on your website.
- In the communication tab of an event, you can set up automated communications for subscribers to an event, like reminders before and on the date of. You can use templates here. Triggering those could be before the event, during, or after the event.
- The questions tab are the information the attendees will have to provide to register to the event. Checking "Ask once per order" will allow the attendee to answer once for everyone in the order. Think of those fields as applying to everyone in the group currently registering.
- The events app, since events are perfect for lead generation, has a Lead Generation configuration view. This view allows you to create rules, which allow you to create opportunities when attendees are created, register to an event, or attend the event. You can set the template of event this rule applies to, as well as any condition (like email existing in the profile, etc). You can assign a team for the new lead, set tags, etc. All of this allows you to create leads automatically as people register/attend events.
### Marketing - Marketing Your Event
- In the Social Marketing application, you can manage your social media campaigns.
- Grouping posts by campaigns allow you to track metrics for a given group of posts, like leads generated, revenue, clicks, etc.
- From a campaign, you can add a post. Choose the social medias, write your message, and schedule it. It will show you a preview for all the medias.
- The questions you set in the event in the Events app will automatically appear on the registration pop-up of your website's event page.
- The attendees smart button on an event will show you all confirmed attendees.
- Events can be public, limited to logged in users, or available via a link only.
- Once people have attended, depending on the lead generation settings you have set up, leads will have been created. This could have happened on registration or attendee account creation, if that's what you set up. The lead will contain the answers to the questions you set up in the Questions tab of the event record.
### CRM - Following up on Leads
- With a filter, you can show leads from only a given event, using a custom filter. Use the "Tags" field that it contains the tags your event had.
### Surveys - Creating a Feedback Loop
- To get attendee feedback, you can create a new survey in the Surveys app.
- You can add as many questions as you like, with multiple answers, single answer… there are many potential question types.
- The description of a question gives your user some guidelines on how to answer; especially useful for free-form answers.
- Once your survey is ready, you can colick share to get a link you can send to people. You can even use the "Send by Email" feature to send it out directly.
### Email Marketing - Sending out Our Survey
- The Email Marketing app uses the same editor as the Website app, keeping the same drag-and-drop flow.
- Same as the website, you can use LLMs to build your email text.
- Once your email's structure is good, set the recipients to the right group. You can even set rules, depending on the fields in your contacts records. You could, for example, target people who attended your specific event, and from which date (so you don't send emails to people who attended years ago, for example).
- You can even link your email to the social marketing campaign we created at the very stop! So that it tracks the clicks and resulting metrics, too.
### Configuration
- For this flow, you'll need Accounting, Invoicing, and SMS Marketing, as well as eCommerce. This is all needed for the ticket registration flow. SMS Marketing is only needed if you plan to send stuff through SMS messages.
- The product type on Event Registration should be set to a Service. And the create on order field should be set to "Event Registration".
- To link the social media accounts, you need to add streams in the Social Marketing app.
- In the Events app's settings, you'll need "Schedule & Tracks" for sessions and sponsors, "Community Chat Rooms" for, well, the rooms, "Tickets with Sale" for selling tickets. You can also enable "Tickets with PoS" when selling tickets from the venue.
## Business Flow - Restaurant
### Planning - Setting Employee Schedules
- You can view schedules by Resource (employee) or by role.
- You can easily move schedules between resources, or, when holding down the control key, duplicate it.
- When schedule conflicts happen, a warning will happen.
- Unpublished shifts appear as striped.
- Shifts with an earmark icon contain a note.
- In the top left, you can use Publish to send the schedule to all employees. You can also use the "auto plan" feature; check the docs for more info.
- If an employee isn't available for a shift, they can send a schedule change request that will need to be approved by a manager.
### PoS - Beginning Your Shift
- Odoo PoS allows you to have multiple views for different rooms in your restaurant; for example, a main floor view, and a patio view.
- You can easily move, remove, and add tables as the plan changes during your shift.
- You can use circle tables, or upload your own floor map. You can rename tables (change their number), or duplicate it with the clone button.
- When selecting a table, you can change the number of seats at a table.
- To order, select a table, and you'll be prompted with the list of items.
- If your product has extras or combos, you'll be prompted with them when you add your item.
- If someone has an allergy or something, you can set a note for the kitchen on the order.
- Finally, you can directly send the order to the kitchen.
### Kitchen Display - Let Them Cook
- In the Kitchen Display app, you can see all the orders from the floor, along with notes and what's been completed already.
### PoS - Splitting the Bill
- When someone wants to split the bill, you can just use the action to do it: select the items to be split, and then pay each order independently.
- When receiving cash, you can add bills directly in the order payment page, so that Odoo calculates the remaining cash needed automatically.
### PoS - Adding Products
- In the top right, you can use the hamburger menu to add new products.
- Make sure to add the barcode to any new products, either using a scanner, a tablet camera, or even manually.
- You can set to track the inventory when needed, add picture, and anything to add to a new Inventory product record.
- Make sure to set the right category for the new product so it's easier to find when selling later.
### PoS - Adding Tips
- When paying, you can use the Tip button to add a tip to the base order.
### PoS - Finishing the Shift
- When closing the register, you'll see a summary of all transactions of the date, allowing you to check the total cash you have.
### Configuration
- In the Point of Sales' app's settings, there are a few things you should configure.
- If the banner at the top of the settings is yellow, this means that you'll have to close the register before making changes to the settings.
- From the settings, you can modify and add floor maps. You can also modify the payment methods.
- You can enable existing payment terminals down in the settings.
- You can also link an IoT box to set up your own terminal.
## Business Flow - eLearning
### eLearning - Creating the Course
- You can build a new course either from the backend, or directly on the website frontend from the "New" button in the top right.
- When creating a course, set your layout, description, and allow people to rate your course or not, and off you go.
- Now you're on the page you can use to build your course: adding sections, content… All of Odoo Website's features are available here!
- Content for a course could be a document, image, article, video, quiz, or certification.
- You can retrieve content directly from a Google Drive account.
- Set the estimated completion time for your resource so that students know what to expect. Finally, publish your resource.
- When creating an article, you have access to all the Odoo Website features to build your lesson contents.
### eLearning - Creating the Certification
- Depending on the content type, data for the content will be auto-populated. For example, titles for PDFs, and duration for videos.
- In the eLearning application, select `Courses -> Certification`. Create a new certification.
- Technically, a certification is really just a quiz, but with a real reward at the end.
### eLearning - Modifying the Course in the Backend
- At all times, select the Course button in the top right to go to the backend view for the course.
- From here, you can change your content, add images, modify the description, options, and karma- stuff?
- Karma defines how many points the user receives on lesson reviewing and course completion.
- You can gatekeep reviewing a course to a specific points minimum, so that not everyone can review content right away. This helps prevents spam from bot accounts.
- For your course, you can change the Enroll Policy to define when someone can enroll. Either it's open, on invitation, or automatic on buying the course itself.
- For paid courses, make sure the policy is set to "on payment", so that you can actually create a product for it, and sell it.
- Smart buttons for a course show sales of that course, attendees to see who's doing it, etc.
- You can link a product to your course directly, so that you can configure your price, type of product, etc. This is needed so that you can actually send the course. Linking it will allow users to actually see and use the course once the product is bought.
- Of course, your course's product has to be published so that people can buy it on your website.
- To publish the course, on the front-end page, in the top right, click the publish button.
### Configuration
- You'll need eLearning, eCommerce, Website, Sales, Survey, Email Marketing apps installed.
- As for settings, you'll need to enable all 4 eLearning settings. These will need some more apps (survey for certifications, email marketing for mailing).
## Business Flow - Online Subscriptions
### Subscriptions - Creating Subscriptions
- In the Sales app settings, you have to enable the Online Payment option to be able to sell stuff online. Also set automatic invoice to on, so that the invoice is automatically sent out, and the revenue automatically logged in the accounting.
- For subscriptions, set the sales and subcriptions tickboxes to on.
- Because subscriptions are set up as sales products, invoices and a ton of other features get enabled, including but not limited to regular invoices for the recurrence of the subscription.
- The `Create on Order` field creates a record, like a task, on a customer buying the product. This way, you can prompt your team to proceed on an order without leaving your customers hanging.
- You can set the cost per unit of measure; if you're making subscriptions for classes, you could have a unit of measure category "working time" that says how many hours are needed internally, and then individual units for an hour, a day, a certain number of classes (example given is 8 classes amounts to 8 hours).
  Not gonna lie I haven't really gotten much of the math in there.
- Cross-sell/upsell products allow you to suggest optional/complementary products on the shopping page of your website.
### Subscriptions - Selling Subscriptions
- Once an order has been completed, it will appear on the backend.
- The default view will only show you ongoing subscriptions.
- The smart buttons will show you the linked records, including tasks that may have been created automatically on order confirmation.
### Subscriptions - Tracking Hours
- In the Timesheets tab of a subscription order, you can set the hours you've spent on working on a subscription (for example, if you're an instructor for a subscribed course). This will compare your working hours with the total allocated time in the subscription order, and update the time remaining accordingly. This will also update a new smart button on the order that will show you the currently logged hours.
## Business Flow - Administrative Department
### Documents - Handling Documents
- Documents has both a tree view, and the usual folders and group by search box.
- You can share documents by adding people or email addresses, and manage general access. You can also copy the link.
- You can upload documents directly, in full resolution without compression on the images.
- On each document, you can add info and tags, which contains the chatter for the document, too.
- Odoo allows you to have email addresses to receive documents on. You set it on a folder, and what it does is that every time you send a document to that email, it will automatically be uploaded to the Documents app, in that folder!
- You can also scan physical documents, in batches too. If you connect your scanner device to your database through the email alias, they will all become automatically sorted as you scan and send them. Neat!
- When scanning multiple distinct documents in a single pdf, you can use the Split PDF feature to split it in different documents. You select the ones that pertain to the type of document you're looking for, then adjust the splits. Finally, you can select the right `Create ...`  button at the top of the screen to create the right records, for example vendor bills, customer invoices, etc.
### Accounting - Handling Bills
- You can use the `Reload AI Data` button to scan PDFs and fill in the fields of a bill or other document. The due date, accounting date, and fields all get filled in automatically.
### Sign - Handling and Signing Contracts
- In the Documents app, you can easily create a contract by tapping the Sign button on top of a document.
- This will show you a list of fields, which you can drag to create your signing form. Kinda like Docuseal and other similar apps.
- Once it's ready, you can send it, or sign it directly if you're with your customer/contractor.
- The customer will receive an email with a sign document button.
- Once all the fields are filled in, the other party will be able to send it back to us.
- Back in the backend, you will receive the response in the Documents app.
- Templates for contracts only appear in the Sign application, not in the Documents app. So, when you use the Sign button on a document, it will create a new template in the Sign application, be sure to check it out over there.
- You can also create a `Request a Signature` activity, by the way.
### Documents - Following Up
- You can create tasks from documents. For this, from the documents app, in the actions menu on the cog, you can select the actions that are available to you from a given document with `Actions on Select`. For example, you could add a button for `Create a Task` which will allow you to create one directly from a document.
- In addition to those standard actions you can add, you can select `Automations` in the cog menu, to create new automations.
- In there, you can, for example, set a task to be created on a given trigger, like adding a specific tag to a document. The example in the video was adding the Presentations tag, which moved the document to the Marketing folder, and creating an activity for that document.
## Business Flow - Construction Project
### Sales - Quotation for a Construction
- For a construction project, you could have invidiual lines for each stage, with the time it takes, an either an hourly or daily fee.
- You could also set UoMs (unit of measure) for weeks or months, if your pricing uses those units instead.
### Project - Managing the ConstructionProject
- When a sales order is confirmed, a project and all related tasks will be automatically created, and, if applicable, using the number of hours defined in your unit of measure and amount in the sales order.
- You can create activities directly from a task in the kanban view.
- You can log hours spent on invidiual tasks to update the amount of time alloted to a specific task left.
- The built-in timer allows you to track your time spent on a task in real-time, using the `Start` button on a task's form view.
### Invoicing - Invoicing the Hours for the Project
- If you go back to the quotation after a few hours have been logged, the hours will have been updated in the `Delivered` column on each line of the Sales Order. This is because we use `Days` as the unit of measure.
- Sales orders have smart buttons allowing you to not only access the related project and tasks, but also the recorder hours so far.
- Careful; hours logged are time sheets. This means they need to be approved by the right people; if hours don't show up in the sales order, that's why.
### Purchase - Buying Material
- When creating a request for quotation in the Purchase app, Odoo will display any On-time delivery data in the `Expected Arrival` field. This may be blank if it's your first time ordering from a given supplier.
- To link your new request for quotation to the current project this purchase will be for, make sure to assign any lines related to that project to the right analytical account. This happens in the `Analytic Distribution` column. Select your project from there.
- You'll need to enable the analytic accounts in the settings for this. And make sure the column is actually visible, too.
### Accounting - Paying our Bills
- From the purchase order, you can create a bill directly. Or, in the accounting app, you can create it directly too.
- Use the `Auto-Complete` feature to select the purchase order and fill in the bill automatically.
- Make sure the analytic account carried over, as well.
### Sales - Invoincing our Customer
- On the same sales order as at the beginning, you can create the invoice. Using the analytic account, the purchase order lines are automatically added to the customer invoice, so that your purchases for their project are automatically linked. Any blue lines are ready to be invoiced (for example, received materials, or delivered hours).
- In the `To Invoice -> Orders to Invoice` view, you can view all sales orders with stuff to invoice.
- When you select orders, you have a button to create invoices automatically. This will create a new invoice with all the blue to-invoice lines.
### Configuration
- For this flow, a few settings and configurations are necessary.
- In the products menu, in the Inventory app, create a service product for each hour worked by your employees (in this case, architects). Set the `Invoicing Policy` to `Based on Timesheets` to link the actual time logged to what you'll invoice your customers.
- Set `Create on Order` to `Project & Task` to create a new project and invidual tasks for the sales order, for when you sell hours of this product.
- When you have a product that you want to pass the cost down to the customer, set the `Re-Invoice Costs` to `Sales price`. This adds a markup to the purchase price. Alternatively, use `At cost` to make them pay the actual amount, without any margin for you.
- Make sure to set `Invoicing Policy` to `Delivered quantities` too, so that your customer isn't invoiced your entire order, just the amount that was delivered for their project.
- For analytic accounts, make sure to enable the feature in the accounting app.
## Business Flow - Airproof
### Inventory - Creating the Products
- Cost for a product allows you to track expenses for getting/building a product.
- In the `Inventory` tab, you can set the `Manufacture` tick to signify that those products are manufactured. Also tick the `Replenish on Order (MTO)` tick to automatically create orders when sales of this product occur. Make sure the `Multi-Step Routes` feeatures is enabled, and that the route is unarchived from the default routes.
### Manufacturing - Building the Products
- You can set bills of materials for each product that you build.
### eCommerce - Selling the Products
- You can modify forms to change their actions, in the Form section of the `Customize` tab on the website editor. You could make it so that filling in the form creates a new opportunity in the CRM app.
### CRM - Taking Care of Leads
- From a lead, you can directly create a quotation.
- You can setup quotation templates to simplify the quotation creation process.
- Pricelists allow you to set promotions, or change pricing depending on time of the year. Pricelists contain rules for determining prices for your products, or percentages applied to your product prices. Either for seasons, different customers, current available stock, you decide what your pricelists mean.
- For shipping, make sure your company has an address and zipcode, and products, a weight configured.
### Manufacturing/Inventory - Fulfilling the Order
- On a manufacturing order, you can use the `Check availability` button to check that all your required materials are currently in stock.
- In `Operations -> Replenishment`, it will list all materials that you need to purchase again. This will create a purchase order in `Requests for Quotation`.
### Sales - Invoicing the Customer
- Once you sent an invoice for a down order, if you want the customer to pay the rest, you can create another invoice for the full amount (the down payment will be deducted automatically).
### Setting Access Rights
- For an intern, for example, you'd set access rights in the `Manage Users` setting.
- It all happens in the `Access Rights` tab. Here, you define what each user has access to, and not access to.
- Check the docs for more info.
### Dashboards - Getting an Overview
- You can filter the metrics for specific products, salespersons, application, etc.
- When switching applications in the dashboards, different filter options will appear.