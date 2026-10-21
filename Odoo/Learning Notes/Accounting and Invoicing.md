# Accounting Basics
## Getting Started
- The fiscal localization depends on the country and its regulations. This is set on database creation, but you can change it in `Configuration -> Settings`. Once you make your first journal entry, you will **not be able to change your fiscal localization**.
- The dashboard has a kanban view with one card for each of the journals. For example, Sales, Purchases, Bank, etc. You can also create new journals directly from there.
- The Customers menu has all options related to customers. Invoices, credit notes, payments, etc.
- Vendors is similar, with similar options.
- In `Review -> Journal Items`, you'll find all entries in your journals. Group by `Journal Entry` to see all individual entries.
- In `Configuration -> Journals`, you'll find all of your journals. These are used to organize your journal entries. For example, sales entries, purchase entries, or bank entries.
- In `Reporting -> General Ledger`, you'll find a view of all of your accounts balanced with debit and credit. You can expand each account to see the journal entries. You can also select a specific period of time.
- In `Reporting`, you'll also find the Balance Sheet, Profit and Loss, and other important reports.
## Chart of Accounts
- The chart of accounts is a list of the accounts a business uses to organize their accounting entries.
- In Odoo, all accounts are categorized based on the financial report to which they belong.
- In the Balance Sheet, you'll find Equity (shareholder accounts, retained earnings), Assets (bank, cash, current and fixed assets), and Liabilities (accounts payable, short and long-term loans, etc).
- In the Profit and Loss report, you'll have the Income and Expense accounts.
- You can modify the Chart of Accounts in `Configuration -> Chart of Accounts`. By the way, the default chart of account differs between countries. If you have a multi-company setup, you can have multiple different chart of accounts for each company, especially if the companies aren't in the same country.
- Each individual account must have a unique code, a name, a type, and whether or not it allows reconciliation with open bank transactions. 
- The best way to create a new account is to duplicate a similar, existing one.
- If an account holds currency different from the base currency of the company, Odoo will automatically convert the amounts in the base currency in order to display them.
- You can set a description for each of the accounts.
## Update the Chart of Accounts
- When you have a lot of edits to your chart of accounts, it's easier to import accounts from a spreadsheet.
- It's best to not replace your entire chart of accounts, so don't change your account ids. If you need to though, make sure your country doesn't have regulations on what accounts you need to group together!
- Also don't change the account_type field willy nilly.
- If you don't need an account anymore, it's best that you deprecate it, instead of removing it outright. Otherwise, you might encounter some pesky error messages.
- To create a new account, just add a new line with a unique code, a name, a type, and whether or not it gets reconciled, and any other fields you have exported (for example, deprecated).
- Do NOT change the account with type `Current Year Earnings`, or even mess around with that type of account in general.
## Import an Opening Balance
> Tough one this one! Might be worth revizing before taking the cert exam :3
### Theory
- If you previously worked with another accounting software before working with Odoo, you'll need to import your history and opening balances.
- Notably, you'll need to import the general ledger, open receivables and payables, the bank balance, as well as the inventory counts.
- It's best to transfer at the end of a fiscal period/year. The general ledger must be balanced, and in general no inconsistency be found in your accounting.
- You can't import a general ledger directly; that would mean the amounts get imported, and then, when you recreate the invoices in Odoo, you'd get double the amount in your income accounts. Instead, you'll need to use a suspense account to hold the amounts that were invoiced/bill before the transfer. This way, you can create the invoices and target those suspense accounts, just for the invoices and bills that were already issued before the import. For any new bills/invoices, you can use the normal receivables/payables accounts.
- For the bank account, you can't import directly either; otherwise, reconciliation will not work when you create new payments. Instead, replace the bank account with the bank outstanding receipts account before you import, or, if its negative, the bank outstanding payments account.
### Practice
- When you create the importing spreadsheet for your opening balance, do one line with the data, journal and reference, and then many lines for the journal items, with accounts and debit/credits. you can't have a debit and credit one the same line, so you'll need separate lines for receivables and payables.
- You can make a sheet for payables and receivables, to import into the bills and invoices models respectively.
- To import an existing balance, use a new journal specific to the opening balance. Type it Miscellaneous.
- Once the journal is created, you can go to Accounting -> Journal Entries to import your journal entry records. The one with the one line per debit OR credit.
- The imported entries will all be under one draft entry, that you will need to post yourself to confirm.
- Once the journal entries are imported, you still need to import the oustanding bills and invoices for the payables and receivables.
- Same thing, go to invoices, import the invoices sheet, and then in bills, the bills sheet.
- The invoices and bills will only include one line. You could technically write all the others yourself, but that takes a lot of time for little returns in actual processes.
- Once the bills and invoices are imported, don't forget to confirm them!
- For the actual amounts, basically, when you import the receivables and payables, you set them in a suspense account, which you then offset by importing the actual invoices and bills (which you need to set the right suspense account in, so that it actually offsets the things).
- To finish the import and balance out the outstanding payments, you'll need to create a transaction for the bank that's of the amount that was imported in your bank account in the general ledger. Create the transaction, label it "opening balance", and set the amount to the one that you imported for the opening balance. Then, you'll be able to reconcile the transaction with the opening journal entry.
# Invoicing
## Issue a Customer Invoice
- Invoices are recorded as journal entries in the Sales journal.
- Invoices have lines for each income and tax accounts (credit side), and receivable accounts on the debit side.
- Invoices can be created directly from sales order, or manually in the accounting app, under Customer -> Invoices, or directly on Sales dashboard item itself.
- You can set a default income account for the sales journal. You can also set income accounts on the invididual invoice lines, or the product itself, or even on the product category. Odoo chooses the most specific account.
- There are distinct tabs for the invoice lines and the journal items that will be in the accounting once the invoice is posted.
- When an invoice is posted by someone that has limited access rights to invoicing (invoicing or invoicing & banks access rights). Only accountants with bookkeeper or administrator access rights can review these. A special, blue button labelled "Reviewed" will appear for those, on these invoices. Once reviewed, it can't be brought back to the "to review" state.
- You can select multiple invoices to post them all at once.
## Customer Invoice from Sales Order
- From a sales order, you can directly create an invoice.
- In the sales order, blue lines are invoicable already. This depends on the invoicing policy: either ordered quantities or delivered quantities. For the first, this means that you can invoice the customer directly on order, and for the latter, only once the products have been delivered.
- When creating an invoice from a sales order, you have multiple options.
	- Regular invoice: invoice all invoicable lines
	- Down payment (percentage)
	- Down payment (fixed amount)
- The invoice will automatically be populated with the invoicable lines from the sales order. Those lines will stop being blue once the invoice has been confirmed.
- If you try to create an invoice without invoicable lines, you'll get an error.
- You can select multiple to invoice sales orders, and create invoices for all of those at once in the actions menu. The Consolidated Billing option groups sales order going to the same customer, into a single invoice to that customer.
## Issue a Credit Note
- A credit note is used to notify customers that they have been credited, for example returning products. Essentially, they are reimbursments, and reduce the amount a customer owes the company. In effect, it's the exact inverse of what an invoice does (a credit in the accounts receivable instead of in the payables).
- In the Sales journal configuration, you can set a "Dedicated Credit Note Sequence", which will separate the sequence (the short code) of invoices and credit notes, adding an R to the beginning of the latter's sequences.
- You can create credit notes on an invoice directly. You'll need to set a reason, and the journal. Going through the invoice sets the right journal automatically, which you would have to do yourself if you created the credit note manually.
- Between Reverse and Reverse and Create Invoice, it depends on what you want to do. The first creates a draft credit note you can edit to reverse parts of your invoice. The latter reverses the entire invoice with a credit note, and creates a new draft invoice that you can remove items from, before sending it out to the customer again.
- Once the credit note is confirmed, it will be posted, just like invoices.
- If the customer hasn't paid the original invoice yet, the credit note will automatically be reconciled and marked as paid.
## Register a Vendor Bill
- From a RFQ, you can create a bill using the right button. Or, you can go to the accounting dashboard, in the Vendor Bills journal, to create manually. From here, the auto-complete feature allows you to bring over a purchase order's info.
- You can also upload a PDF of one of your bills, and Odoo will digitize it to fill in the date, vendor, and invoice lines full with quantity, price and tax.
- Once the bill is posted, a sequence gets assigned, and a journal entry is added.
- The bill date is the date the invoice was issued at. The accounting date is the date the invoice was posted in our accounting at. The accounting date will be the first possible date after the lock date of the fiscal period; for example if you post an accounting date after new year's, when the invoice was issued last year (I think).
- The bill will stay "in payment" until a bank transaction is reconciled to it.
- Email aliases allow you to receive bills sent from your vendors directly to your database. This is set up in the Vendor Bill journal's configuration, under Advanced Settings.
## Vendor Bill Digitization
- You could configure a scanner to send the scanned documents to an email alias in Odoo. This way, bills get automatically uploaded to your Documents app in the right folder.
- If you scan multiple pages, you'll find that the uploaded document contains all pages under one doc. You'll need to use Odoo Documents's split feature to split the pdf into mulitple bills.
- Once the pdfs are split in the split feature, use the create vendor bill button to create the bills directly.
- Optical Character Recognition or OCR will populate the bill's data directly from the PDF, using in-app credits.
- Accounting Accounts are automatically selected based on historical data: which account was the most used for this vendor, with this particular invoice line.
- An asset will be created automatically, if applicable.
- Odoo will create one invoice line for each tax rate.
- Odoo will flag potential duplicates of bills, too. You can delete the one that you don't want.
## Payment Terms & Terms and Conditions
- In the Accounting's configuration, you can access the Payment Terms. Those allow you to configure the times and conditions for paying invoices for your customers.
- You can for example create a payment term with two payments, where you'd create two Due Terms lines in the payment term configuration. You can also enter a written explanation of the payment terms so that it is clear on your actual invoices.
- You can hide the installment dates of the invoices on the actual documents.
- Terms and Conditions are different from payment terms. They need to be activated in the Accounting Settings, as they are a feature. The text is also set directly in the settings for when they are pretty short.
- If the T&Cs are too long, you can add a link to a webpage instead, where you can paste whatever text you want to have. Then, you can preview your new page.
# Payments
## Payments and Outstanding Accounts
- "In payment" means that the bank reconciliation process hasn't been done yet, but that the full amount has been received.
- Outsanding payments/received accounts are used at temporary holding accounts, between the time that the payment is registered in Odoo, and the reconciliation with the bank statements. This way, the payment is put into the outstanding accounts, and when the payment is reconciled, it balances out. This provides better visibility into your accounting, because the outstanding receipts will give you a view of all incoming payments that you've registered but haven't reconciled yet.
  Essentially, outstanding accounts are just here to allow you to see what's going on before the payments get reconciled, so you get a more up-to-date view of your customer's payments.
- Worth noting that not putting outstanding receipts/payables accounts in the configuration will stop Odoo from creating those journal entries on payment creation.
- In the Bank journal configuration, in the Incoming/Outgoing payments, you can set payments methods and their outstanding accounts.
- You can select multiple invoices to group payments. This allows you to group payments per partner, which means that all invoices under the same partner will have just one payment entry. Separate partners will still have their own payment.
- Creating a payment from an invoice will automatically match the payment to that invoice.
- You can also create payments manually from the customers or vendors menus depending on what kind of payment it is. When you do that, an oustanding credits/debits banner will appear on the bill/invoice form view, where you'll be able to link your new payment to that document.
- You can also link manual payments to documents in the accounting -> reconcile view. This only works when the payment creates a journal entry, thus when the payment terms have an outstanding account set. Also, this is only reconciling between the payment of your document, and the actual document. We're not reconciling any bank transactions here.
- You can skip bank reconciliation if needed (for example on a cash journal). For this, go to the relevant journal, in the incoming payments tab. set the outstanding account to the journal's account itself, both on the outgoing and incoming payment methods. Then, when creating a payment, use your journal as the payment method. This skips the "In payment" step of the document, where you'd usually reconcile, putting it as "Paid" directly.
## Online Payment
- Online Payments are a feature that needs to be turned on, under the Accounting settings `Invoice Online Payment`.
- You'll see available payment providers in the accounting app configuration.
- You can limit availability of payment providers based on maximum amount, currencies, and countries. You can also choose the journal for the payment method.
- You can customize the feedback messages per payment method, for pending payments, completed payments, etc.
- Online payments won't get reconciled to the bank statements automatically.
## Customer Payment Follow-Up
- In `Accounting -> Configuration -> Follow-up Levels`, you can configure the follow-ups that trigger after a specific number of days.
- You can switch the when and how of follow-ups. You can choose for it to be automatic, attach invoices, or add followers.
- Follow-ups allow you to schedule activities on a follow-up triggering.
- In the customer form view, in the `Accounting` tab, you'll see the status of all invoice follow-ups levels for that customer. From here, you can see the individual `Journal Items`, use `Send` to send a reminder. You can set the reminders to `Automatic` here. Worth noting it needs to be set both here and in the follow-up level to `Automatic`, for it to actually be automatic.
- The `Follow-up Report` shows you the current status of follow-ups for that customer. This is also what the customer will see when sending out a follow-up.
- You can select multiple customers to `Process Follow-up` for all of them.
## Cash Discounts
- Cash discount is when a customer can pay early to get a discount. This has some tax implications.
- In `Accounting -> Configuration`, you'll find the `Cash Discount Gain` and `Cash Discount Loss`. This is where you define the accounts that will hold all amounts related to cash discounts.
- In `Configuration -> Payment Terms`, you need to check the `Early Discount` checkbox for a percentage and a time limit.
- Each term can use a specific tax reduction. You could reduce the tax on early payment, never, or always. This will make the tax tags automatically be updated by Odoo depending on the final amount, if there was a cash discount.
  If `Always` is set, the tax will always be reduced, even if the customer doesn't pay early. `On early payment` only reduces the tax if the early payment was done, and `Never`, well, never reduces the tax. This depends on your country or region.
- If you register a payment before the end of the early payment date, it will automatically apply the discount, and give you a banner that says so on the `Register Payment` popup.
# Bank and Cash
## Bank Configuration
- First, let's understand the flow of payment for an invoice.
	1. You confirm the invoice. Account receivable <- Income, taxes
	2. You register a payment. Outstanding receipts <- Account receivable
	3. You create a bank transaction. Bank <- Bank suspense (temporary account before reconciliation)
	4. You reconcile the bank transaction. The previous journal entry gets its Bank suspense credit account replaced with the Outstanding Receipts account, balancing it all out.
- In the Accounting settings, you'll find in the `Default Accounts` section four accounts for bank transactions: `Bank Suspense`: the temporary bank transaction account from step 3 above; `Oustanding receipts`: holding account for customer payments for step 2; `Oustanding Payments`: holding accounts for vendor bills, for step 2 as well; `Internal Transfer`: used to balance entries from one bank or cash account to another.
- In the bank journals, each journal must have a unique bank account. Multiple journals can't share the same account.
- In the bank journal configuration, you can override the default accounts found in the settings.
- You can set outstanding accounts for incoming and outgoing payments' payment methods for a bank journal. Just unhide the setting in the list view in the tabs.
- The IBAN number is required for when you want to generate SEPA and NACHA stuff.
## Bank Transactions & Bank Synchronisation
- You can create bank transactions manually, import them, or even synchronize with the actual bank.
- Transactions with a checkmark are reconciled.
- Each transaction has a chatter, and can have activities and attached files.
- Statements are groups of bank transactions. You can create statements from any bank transaction, which will create a new statement for this transaction and all the ones before it, up until the last statement. You can attach pdfs to statements.
- When synchronizing a bank account, Odoo will automatically pull in all transactions from that account. You can connect banks from the accounting dashboard's bank journal. This uses a third-party provider.
- If you don't want or can't sync, you can import bank statements yourself! In the journal, you can click the upload button to import an excel file, or a statement pdf, which Odoo will read.
- You can also create transactions manually, where you assign a partner, amount, and label.
- You can't edit transactions that have already been reconciled. De-reconcile them first.
## Bank Reconciliation
- Reconciliation is when you validate your bank transactions, matching them to an existing payment, or manually, to an account.
- Bank transactions create journal entries. These are usually one side to the bank, and the other side to the suspense account. By default, the latter acts as a temporary holding account until the transaction is reconciled, after which it will be replaced with the account from the payment or the account you manually reconciled with.
- A reconciled items smart button will appear when a transaction has been reconciled. And the suspense account will be replaced, too.
- On the transactions list view, you'll see unreconciled transactions with different buttons depending on the transaction.
	- Transactions with no partner will have buttons to suggest setting one, or setting the account directly.
	- Transactions for a partner that has open invoices/bills, Odoo will suggest the Reconile button, where you match the transaction with those documents.
	- If the partner doesn't have any open invoices or bills, Odoo will suggest either Receivable or Payable, depending on whether the transaction was incoming or outgoing. This writes the amount directly to the receivable/payable accounts.
- You always have access to all buttons from the three dots buttons.
- Reconciled transactions will have a checkmark instead of buttons.
- Odoo has a hard-coded condition for bank reconciliation: if two out of three fields match between partner, label, and amount, Odoo will reconcile the transaction with the matched document automatically.
- You can set a range for differences between the actual invoice and the transactions for it to still be reconciled automatically. This gives some leeway for processing fees differences, and still allows you to reconcile transactions easily. When that happens, you can always choose to set the invoice to only a partial payment instead, or vice-versa.
- You can delete invidual matches for a transaction without deleting the transaction outright.
## Bank Reconciliation Models
- These are customizable rules to identify transactions and match them according to other entries in your db.
- This happens in the bank journal configuration, under bank reconciliation models.
- Odoo has a hard-coded condition for bank reconciliation: if two out of three fields match between partner, label, and amount, Odoo will reconcile the transaction with the matched document automatically.
- There are two types of reconciliation models. Manuals are ones that are suggested under the `Reconcile` button on transactions, while automated models are executed automatically without user intervention.
- The order of reconciliation models defines the order Odoo will check them to match a transaction. It will apply the first automated rule that matches.
- In each model, you can set the rules, including the journal, partners, amounts, labels. Leaving those blank applies to all entries for that rule.
- The counterpart items are the journal items that will be created when you use this model. You can set amounts by percentages, set a label, and of course choose the accounts. You can have as many lines as you wish.
- Amount distribution can be fixed, percentage, or even from label!
- Odoo will create reconciliation models automatically when noticing that similar transactions are reconciled in the same way. You can see those by going to the reconciliation models, and removing the `Created by user` filter.
## SEPA Credit Transfer
- SEPA is the European transaction system. It standardizes cashless payments in Europe, in Euros.
- There are two types of SEPA payments in Odoo: outoing (credit transfers) and incoming (direct debit).
- You usually submit payments to make to the bank via batch files.
- In Odoo, this is configured in the Accounting Settings. It's a feature that you need to enable, both for credit transfers and direct debit if you use them. Enabling the feature creates a payment method in the bank journal.
- You'll need to make sure that the IBAN number is entered in the bank journal configuration as well.
- To create a batch, select SEPA payments that you made, and validate it. It will generate an XML file that you can then upload to the bank portal to execute the payments.
## SEPA Direct Debit
- Direct Debit is the way for you to withdraw money directly from your customer's account. You'll need a direct debit mandate to do that. This is simply an authorization from the customer. This makes it so you don't have to wait for the customer to actually send the money.
- This is configured in the accounting settings, as you need to enable the feature, inputting the creditor identifier. In `Customers -> Direct Debit Mandates`, you'll need to create your mandates for your customer. This has the customer, IBAN, and the journal that you'll use. The latter has to have a bank account set up. The SDD Scheme depends on the type of customer; CORE is for B2C, B2B is, well, for B2B. The mandate has to have a start date, but the end date is optional. Don't forget to set the company if your db is multi-company.
- You can filter invoices based on your SDD mandates to only see the ones you have a mandte for. You can register payments for those directly; don't forget to set the SEPA DD payment method on the payment!
- Then, you can create the batch payments to validate and then upload the XML to your bank for it to execute them.
- You don't need to reconcile items individually, you can use the batch payments tab to reconcile transactions easier.
# Taxes
## Taxes and VAT
- This is configured in the accounting settings. You can default tax rates, automatically populated based on the fiscal localization. You'll also set the rounding method.
- In `Configuration -> Taxes`, you can see and modify all available tax rates.
- You can set individual tax scopes, to set if a tax should apply to goods or services, or empty for both.
- The tax computation can be a fixed amount, a percentage, or even a python expression if it's more complicated.
- The distribution lists are for which tax account should receive amounts, and how much for each amount.
- Enable `Include in Analytic Cost` to include the tax costs in analytic reports.
- For a product, you can set both a tax for selling to customers, and a tax for buying from your vendor.
- You can also set default taxes for income/expense accounts.
## Cash Basis
- These taxes are reported based on when payments are made, rather than when invoices are confirmed and a payable is created. This is mandatory in some countries and under some conditions.
- This is a feature you have to turn on in the settings. You can set a default journal and account for it if you will.
- In `Configuration -> Taxes`, you'll configure your cash basis taxes. You set it in the `Advanced Ooptions` tab, in the `Tax Exigibility` to `Based on Payment` instead of `Based on Invoice`. Set a transition account to hold the amount between the invoice confirmation and the actual payment.
- With cash basis taxes, confirming an invoice doesn't have an impact on the tax report. It only happens when the payment actually arrives, which is the point of cash basis. For this, it just doens't use the tax tagss for the invoice when it is posted.
- When you create a payment for the invoice, the journal items will use the tax tag this time, which will impact the tax report.
## Fiscal Positions
- You configure them in `Configuration -> Taxes`. In each tax, you'll see the `Fiscal Position` field. For sales to other countries where you'd remove the VAT from your country, set this field to `Intra-Community`. The `Replaces` field sets the taxes to replace when selling to the `Fiscal Position` that was set. For example, if you put `21%` in the `Replaces` field and `Intra-Community` in the `Fiscal Position`, any sales that would be made to a partner in `Intra-Community` with a tax of `21%` would instead get replaced with the current tax you have open.
- You can list all the fiscal positions in `Configuration -> Fiscal Positions`. From a recordj, a smart button can lead you to all taxes applied to this fiscal position.
- `Account Mapping` allows you to replace the accounts that would be used for sales or purchases with the relevant ones for that fiscal position. For example, instead of domestic accounts, setting the intra-community accounts for international sales or purchases.
- `Legal Notes` allow you to add text to invoices using this fiscal position.
- `Detect Automatically` assigns a fiscal position automatically based on the fiscal position's config below the field. For example, requiring VAT, based on countries or country groups, or even ZIP codes.
- If you need to handle a specific contact differently, you can go to the contact, in `Sales & Purchases`, and assign a `Fiscal Position` manually.
- You can even be more specific, by setting the `Fiscal Position` in an invoice directly, overriding both the contact and configuration fields.
## Tax Report and Return
> Needs some reviewing, I'm still not very clear on tax stuff
- Generating tax reports' processes depend on countries and regions.
- Odoo provides a dedicated journal for tax returns. You'll need to set it up though. In the accounting app settings, you can set the periodicity for your business, and the journal. One should already have been set by default by Odoo.
- `Configure your tax accounts` allows you to set tax payable/receivable accounts for each tax groups. These are essential to automate the tax closing process, so make sure they are right as per your contry.
- On the dashboard, once periodicity is configured, you'll be able to click the `Tax Returns` button to set the accounting periods. This marks the beginning of when the tax returns periods will be created. Once you apply these, you'll receive automatic reminders for the tax returns.
- Then, the tax returns button will show a chronological list of to-do tax returns. You can remove the filters to see the complete ones and future ones. There's also a calendar view.
- Each tax return has three steps: review, submit, and pay.
- Odoo does many validation checks automatically to make sure a tax return is ready for submission. For example, attachments, company data, draft journal entries leftover in the accounting, etc...
- You can set a validation check "supervised" status to signify that a human reviewed the check.
- You can create your own automatic checks in developer mode, in the configuration menu.
- Once you validate that all checks have succeeded, you can validate and lock the tax return. This will switch the tax return to `Review` state. Validating means you're posting the closing entry, and that you're setting the lock date.
- In `Accounting -> Lock Dates`, you'll see the current lock dates. This prevents users modifying entries with tax accounts, so that the tax report stays the same for the period before the lock date. The lock date is automatically set when validating the tax report for that period.
- Once the tax return has been validated, you can submit it through the tax return button, and going on the tax return intself. You can download the report as a PDF or Excel file, and then submit it to your government authorities.
- Clicking `Submit` gives you submission instructions for the fiscal localization of your database. Usually, it's downloading the xml and submitting it to your government.
- Then, `Mark as Submitted` shows you a payment form if a payment is due, again, based on your country regulations. After that, the tax return will be marked as `Pay`.
- Subsidiaries share the fiscal period, but not the lock dates.
- If you create an invoice/bill with taxes before the lock date, the accounting date will be automatically set to the first date after the lock date. A banner will inform you when that happens.
# Accounting Management
## Extra Taxes
- Extra taxes is a term for any taxes beyond the basic taxes imposed by your government. This could be a luxury, environment, import or export tax. The method to compute these varies from country to country; make sure to configure yours based on your country.
- You can apply multiple taxes to a product or price. However, some taxes depend on others depending on your government's regulations.
- For this, you should have `Affect Base of Subsequent Taxes` turned on on the tax that will affect other taxes, which will make the current tax affect the calculation of subsequent taxes in the list.
- Then, put the taxes in the right order in the taxes list, so that the sequence is correct from top to bottom.
- For example, if you need tax A applied before tax B, you'll set the `Affect Base of Subsequent Taxes` to on in tax A, and make sure it is listed before tax B in the list view of taxes. This way, tax B will computed from the total price + tax A, instead of just the total price.
## Asset Creation and Management
- Company vehicles and laptops are also assets, not just buildings. These assets depreciate as they age, so it's best to track this loss of value by making journal entries regularly. Odoo allows you to manage this automatically.
- In `Accounting -> Assets`, you can create assets. Set the original value, the date of acquisition, and the not depreciable value (salvage value). The difference between the original value and the not depreciable value is the value that will depreciate.
- You can set the depreciation method:
	- Straightline makes your asset lose a fixed amount per period.
	- Declining uses a percentage instead of a fixed amount
	- Declining then straight line does both
- Careful: setting the period to 12 months or 1 year isn't the same. The unit sets the periodicity of journal entry creation: if you go down to months, an entry will be made each month, but if you set it to years, only one entry will be done per year.
- The computation determines the way of calculating the periods: `Based on days per period` helps for months that have fewer days, allowing for greater precision. `No Prorata` is just like `Constant Periods`, but with the added strictness of having no prorata rate, which will remove the field entirely. This removes the prorata that happens in the first and last period of the depreciation entries.
- Then, you set the accounting details of how the depreciation will be represented.
- You can link a new asset to existing vendor bills.
- `Compute Depreciation` computes the future journal entries for the depreciation of your asset. If a line has already been posted, the journal entry label will appear too. The smart button at the top also shows you all posted entries. Any draft entry will be posted automatically when the date is here.
- In `Reporting -> Depreciation Schedule`, you can find a report for the depreciation of your assets.
## Asset Models and Automation
> Asset models have been replaced by depreciation models as per 19.2.
- Asset models are basically templates for assets, with pre-filled settings for accounting and depreciation details. These only work for non-current assets and fixed assets.
- They are configured in `Configuration -> Asset Models`.
- The asset model form view is basically just the asset form view, without the value-related fields, since those change depending on the asset. What's common between assets under a given model is the depreciation system and accounting details.
- To finish configuring your asset models, you'll need to go to the fixed assets account, and in the account configuration, you'll go to the `Automation` tab. You can set it to automatically create assets when the account is used, for example, when a bill is issued for a fixed asset account, which would mean that a new asset has been acquired. You can either create the asset in draft, or create and validate. To validate automatically, you'll need an asset model linked.
- In the `Automation` tab, the `Manage Items` checkbox determines whether individual assets should be created if multiple were bought, of if a single asset should represent the group of items bought.
- The assets will only be automatically created from a bill once the latter has been confirmed. A smart button will appear for that bill.
## Expense and Revenue Recognition and One-Shot Entries
> Very iffy understanding on my side, will need reviewing
- Expense and Revenue Recognition is also known as just "deferred entries".
- "Deferred payments" is for revenues or expenses that happen before a good or service has been delivered.
- "Acrued payments" is for revenues or expenses that happen after a good or service has been delivered.
- Both of these are payments for something that applies across a period of time, that must be represented in periods. For example, a yearly Odoo subscription must be split evenly across the year, with monthly records. All in all, the two above concepts help shed clariry on the company's accounting.
- One-Shot entries are one-time recurring entries, and thus aren't split periodically. Instead, they are split in two, between the start date, and the recognition date.
- In the accounting settings, you can configure default accounts for deferred entries. You can also set the journal for those entries.
- You can also set when to generate expense/revenue entries, and how to compute the amount (based on days, or equal per month regardless of the amount of days in that month).
- To set deferred entries for a bill or invoice, you can set a start and end date for each bill/invoice line (you'll need to stop hiding the fields in the table), and the entries will be calculated automatically once you confirm the document. A smart button `Deferred Entries` will appear to show you the deferred entries.
- If you want to make one-time entries, you can go to a confirmed document's `Journal Items` tab, and use the `Cut-Off` button. The latter is only present for income/expense accounts. In the pop-up, you will set the recognition date (when the document will be issued??), the accrued account, which will be used for the accrued entry, and the adjusting amount (for example, 50% if you want to recognise an invoice/bill's half for this fiscal period, and the other half for the next fiscal period).
- You can also handle multiple bills at once: select entries that all have the same type of account, either all expense, or all revenue. Then, use the `Change Period` action. Again, you select the date, account, amount, and you're good to go for all of those entries.
## Analytic Accounting
- Analytic accounting helps tracks costs and revenues, per project or asset.
- Analytic accounting is a feature that needs to be enabled in the settings.
- In `Configuration -> Analytic Accounts`, you will find all analytic accounts. Analytic accounts are what is used to track your expenses and costs, and anaylitic plans are to give some structure, basically like folders.
- `Default Applicability` determines when we can or have to use this analytic plan on journal items. It can either be optional or mandatory, or even unavailable.
- The `Applicability` list fine tunes the application of this analytic plan; you can set a domain, like bills, a prefix for accounts, product categories, and whether the applicability is mandatory or not.
- The `Subplans` smart button is for creating a parent-child structure in your analytic plans.
- The `Analytic Accounts` smart button shows you the current accounts assigned to this analytic plan.
- To actually apply the analytic accounting setup you have, you'll use the `Analytic Distribution` under bill and invoice lines, where you can set the repartition according to the analytic plans (columns) and analytic accounts (value in each cell).
- Once the repartition is done, you can even create a model for it, so it can easily be reused in the future. You can set conditions to meet to use this model, for example, a partner, or account prefixes, or specific products or product categories.
- If you try to confirm a document and an analytic plan is mandatory, and you haven't filled it in, you'll get an error. Same thing if the sum of all values in a line of the analytic distribution isn't 100%.
- You can't update a document's analytic distribution once it has been confirmed; however, you can still edit the individual journal items' distributions. This is also where you'd mass-edit them if needed.
## Analytic Budgets
- You'll need some analytic accounts set up to create analytic budgets.
- You'll also need the `Budget Management` feature in the settings.
- Then, `Accounting -> Budgets` is where you'll work for this.
- You can have budgets for expenses, revenues, or both. This sets the type of lines that will be present in the budget.
- You can revise budgets in two ways: resetting to draft and modifying it as is, or `Revise` it, which is a bit more transparent because it will create a new budget with the `REV` tag prepended to its name.
- The `Achieved` column in the budget is the amount found in the linked analytic account, the money you've actually spent using that account.
- The `Committed` column is the amounts purchased, but not yet billed, plus the `Achieved` amount. Basically, the amount of stuff you have in purchase orders that don't yet have an associated bill.
- The `Theoritical` amount is the amount you should have achieved based on the progress of the budget's period.
- A red line in a document like a bill will indicate that this particular line make us go over-budget. This works thanks to the analytic accounts linked in the analytic repartition, and the budget that uses them.
- From a document that is linked to a budget through the analytic repartition, a `Budget` smart button will appear to see a pivot table of the budget related to the document. In the pivot table, you can click on any amount to see the items that contribute to this amount.
- In the budgets list view, the `Generate` button will allow you to generate periods for a budget you have selected. Basically, this will split the selected budget in the specified periods in the pop-up.
- You can see budget lines for all selected budgets using the `Budget Lines` action. This allows you to create graphs, pivot tables, etc.
## US Tax Compliance - Avatax
> Didn't watch this one, it's hardly relevant to my work here in Switzerland
- Basically an api link to a popular tax service??
# Reporting
##  Multi-company and Branch Management
- A company's branches receive the same chart of accounts and journals, but branch-specific journals can be created. The main company also manages the fiscal periods for it and its subsidiaries, as well as the lock dates. Branches can have a lock date prior to the parent's. The main company can access documents from all branches, but branches only access their own records. The main company and branches must be in the same country.
- You can restrict users' access to specific companies in a multi-company setup.
- The `Inter-Company Transactions` feature allows you to automatically create documents when trading between your different companies. For example, generating bills and refunds, sales orders, or purchase orders.
- You can have the same account used by different companies, and you can even merge accounts between companies.
- There are two ways to set it up: for a new account, set the mapping of an account to the account of the other company you want to link with (which will be created if it doesn't already exist). Then, set the company field to the two companies that will share the account.
- The other way is through the merging tool: with two companies selected, in the chart of accounts, select the two accounts from different companies you want to merge. Then, use the `Merge accounts` action. The new account created will have both companies assigned.
- You can unmerge accounts if needed. It will tell you which accounts will be available again once you unmerge.
## Financial Reports
- The `Reporting` menu is where it all happens.
- The Balance Sheet is a snapshot of your company's position at a specific date, full with assets, liabilities and equity. You can use the country-specific balance sheet, or a generic one.
- You can compare reports to different periods, which will make a new column appear.
- You can set many filters, including limiting reports to specific journals.
- You can also add draft entries, hide lines at 0, etc.
- From reports, you can access individual items and their chatter.
- On the Profit and Loss report, you can add budget information using the appropriate button.
- You can modify budget amounts from a report displaying the budget directly.
- You can download reports as pdfs or excel sheets, or copy them to documents in Odoo. For the annual statements, all three files are downloaded and saved in a single file.
- In `Review -> Journal Audit`, you'll see a report on journals and their accounts. You can modify journal entries from drilling down in specific accounts, including changing the account for an entry.
- In `Review -> Annual report`, you can create a new annual report for your company. All relevant documents to your country will be added automatically. The report will be stored in the private folder in the Knowledge app. You need to toggle documents for them to be added in the final pdf report. All dates and field values will be automatically updated when the final report is generated.
- Other documents might have links to reports on the accounting app. You can customize those links to change the reports that they point to, including the filters and general settings for that report, just like you would if you were on the report directly.
- You can load additional templates if necessary, to add stuff to your report. You can also add, move around, or remove individual documents or articles.
- Supporting documents are for external pdfs that are to be added to your report.
- To download your report, go to the main page containing all the documents, and use the downlaod feature.
# Inventory Valuation
## Inventory Valuation
- Costing methods are different ways of managing your inventory's valuation as they enter and exit your inventory.
	- Standard cost is when you set the value of the product right on the product record. It will always have that value regardless of how much you pay for it.
	- AVCO (average cost) is where the cost of all of your inventory is averaged as they enter your inventory.
	- FIFO (first in first out) the value of the first unit that enters your inventory is the value that is first to leave as you extract stuff from your inventory.
- Removal strategies are for determining which physical units are the next ones when removing stuff from your inventory.
- Other factors also might affect your company's valuation: continental or anglosaxon accounting, or manual or periodic valuation methods, vs automated or perpetual method. The former is the accountant manually making journal entries about the inventory, while the latter lets Odoo do the work for us.
- The costing method is set on the product category.
- You also set the inventory valuation method there (automated or manual).
- In `Reporting -> Valuation`, you can see inventory valuation per product. This is possible regardless of whether you use automated or manual inventory valuation.
- It might feel weird to only base your valuation on a fixed amount is as is the case with standard valuation, but some companies actually use this to compare their expected costs to their actual costs.
- FIFO doesn't necessarily match the actual products that left your physical inventory. In the accounting, your first unit sold might not be the actual unit you sold in the physical inventory. They aren't linked like that.
## Inventory Valuation (Continental)
> The whole continent/anglo-saxon thingie has been scrapped in 19, you have to set the inventory valuation method instead between periodic and perpetual. The machism is still there, but the execution is very different, so I'm taking minimal notes on this one.
- In the continental inventory method method, the cost of a good is taken into account as soon as it enters the stock.
- You'll need the db to use continental accounting for this, not anglo-saxon.
- Purchase orders don't create journal entries. The bill does.
- Make sure the automated accounting feature is on, and that the `Inventory Valuation` setting of your product category is set to `Automated`.
- With this method, the accountants need to make sure to enter products into balance sheet if they aren't sold quickly enough so that the accounting reports don't drift *too* much.
## Inventory Valuation (Anglo-Saxon)
> See note in the previous section.
- Used primarly by english-speaking countries like the US, UK and Canada.
- The difference with Continental is that the cost of goods are only recognized once they have been sold instead of as they enter the inventory.
- Make sure the automated accounting feature is on, and that the `Inventory Valuation` setting of your product category is set to `Automated`.
# End of Period
## Multi-Currency - Realized Gains/Losses
- Realized gains/losses are when currency rates change between the time when you receive/send a bill/invoice, and when the time to pay comes. For example, you might have sent an invoice for 100 dollars, but the dollar rate goes down in between and now the actual amount you'll receive from the 100 dollars will be less in your home currency. That's a realized loss. For the opposite, think of a bill in dollars that you pay only after the rates have lowered; you'll have a realized gain.
- "Realized" means that we've actually registered a payment; you can't dispute it.
- Odoo Multi-currency allows you to automate the process of taking realized gains/losses into account.
- The `Automatic Currency Rates` feature in the Accounting app allows odoo to automatically update exchange rates on a regular basis which you decide (you can actually choose manual if you don't want to sync automatically). You also choose the bank from which the sync will happen.
- Still in the settings, you can access the list of currencies and active the ones you'll use. For each currency, you'll have a list of rates as updated by your automatic currency rates feature.
- Odoo automatically converts foreign currencies to your own currency in your documents. It uses those rates to do that. Basically, you use your main currency to create your documents, and depending on the document's currency, Odoo will do the conversion automatically. You could have an invoice in Dollars, but the Debit and Credit amounts will still be in your home currency.
- When you add a payment for a document that was in a foreign currency, Odoo will automatically create an exchange journal entry for the different in exchange rates between the document's posting date and the payment date. That's if you actually do the configuration correctly.
- If you also have a bank account in a foreign currency, you'll also need to configure it correctly. The currency for the journal and the bank account need to be set correctly. Odoo will convert other currencies that the journal's into that currency, even if the journal has a different currency than your home country's.
- In the case of a bank account in another currency, Odoo will not create an exchange entry automatically, you'll have to do it yourself.
## Unrealized Gains/Losses
- Unrealized gains and losses are still about the exchange rates changing over time, and thus the real amounts paid/received for documents changing, but this time, it's not about when the document gets paid.
- Instead, unrealized gains and losses need to be accounted for when closing the fiscal period, to represent accurately the current state of accounting at that time of the year. These gains/losses are uncertain, contrary to the realized gains/losses.
- In odoo, this has to be done using a manual trigger, and you'll need to reverse the entry at the beginning of the new fiscal period.
- The specific report you need is found in `Accounting -> Review -> Regularization Entries -> Unrealized Currencies`.
- Then, in this report, use the `Adjustment Entry` button to generate this entry and the reversal entry. These will automatically be posted on the dates you determined.
- Make sure to set the reversal entry to the first day of the new fiscal period.
## Closing the Fiscal Year
- Best practices for year closing:
	- Bank accounts fully reconciled
	- Matching book balance and bank statement balance
	- Customer invoices and bills have been created
	- Draft entries confirmed or cancelled
	- Expenses accurate, and validate them
	- Received payments encoded and confirmed
	- Close all suspense accounts
	- Loans registered for automatic ammortization calculations
	- Review overdue payable and receivables
	- Assess whether provisioning for uncertain liabilities or other stuff is required
	- Book depreciation and deferred revenue entries
- The balance sheet is automatically calculated by Odoo; with an unallocated revenue signifying your revenue for the year. All that's left to do is to allocate it.
- In the accounting settings, make sure your fiscal year end date is set to your company's needs. If you need to edit fiscal years manually because of starting in the middle of the year, or having a fiscal year longer than 1 year, enable the Fiscal Years feature and edit from there.
- In `Report -> Profit and Loss`, you'll find the profit and loss statement. You'll see your profit or loss here; this amount is also found in the balance sheet, labelled as `Unallocated Earnings/Losses`.
- To close, copy the profit/loss amount. Then, create a journal entry on the last date of the fiscal year according to your fiscal localization's accounting standards.
- After this, the unallocated earnings line of the balance sheet should be at 0.
- Then, you'll need to use the annual closing feature to complete the process. In the tax returns journal, you'll find the annual closing tax return. This has a lot of checks for annual closing; some of those are automated. If one of these are anomalies, you should fix it before closing the year.
- Once all checks are reviewed or supervised, you can validate the report.
- You can add your own checks if you need, under developer mode and `Configuration -> Checks`.
- You can reset a report if it has been validated.
- When you submit, you'll see fiscal localization-relevant instructions for submitting an year-end report.
- The, you lock the fiscal year in `Accounting -> Lock dates`. There are five dates:
	- Sales Journal lock date prevents creating new invoices and journal entries after closing. Any invoice posted after this date will have an accounting date in the next period.
	- Purchase journal lock date is the same mechanism but for vendor bills.
	- The lock tax return date ensure no journal entries affect tax accounts before that date (this is automatically set when you validate your monthly tax return)
	- The lock everything date prevents all journal entries, setting their date to after the fiscal period end instead.
	- These are all reversible with accounting/admin rights; you can set exceptions if you need to make a quick change. All of it will be logged into the chatter of the company record.
	- The hard lock isn't reversible at all; this is necessary for some countries, not others. Don't use it if it's not standard to lock your accounting at the end of the fiscal year in your country.