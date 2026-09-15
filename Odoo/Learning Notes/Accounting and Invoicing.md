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
### Theory
- If you previously worked with another accounting software before working with Odoo, you'll need to import your history and opening balances.
- Notably, you'll need to import the general ledger, open receivables and payables, the bank balance, as well as the inventory counts.
- It's best to transfer at the end of a fiscal period/year. The general ledger must be balanced, and in general no inconsistency be found in your accounting.
- You can't import a general ledger directly; that would mean the amounts get imported, and then, when you recreate the invoices in Odoo, you'd get double the amount in your income accounts. Instead, you'll need to use a suspense account to hold the amounts that were invoiced/bill before the transfer.
- For the bank account, you can't import directly either; otherwise, reconciliation will not work when you create new payments. Instead, replace the bank account with the bank outstanding receipts account before you import.
### Practice
- 