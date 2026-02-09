---
tags:
port: "143"
---
IMAP is an internet standard protocol that is used by email clients to **retrieve email messages from a mail server**.
These clients use a [[Transmission Control Protocol]] over [[Internet Protocol]] connection.
# How it works
Instead of the server being just a temporary stop before emails get retrieved like in [[Post Office Protocol]], IMAP servers use quite a bit of storage, as they keep emails and their states unless otherwise specified.
## Commands
- `LOGIN <username> <password>` authenticates the user
- `SELECT <mailbox>` selects the mailbox folder to work with
- `FETCH <mail_number> <data_item_name>` Example `fetch 3 body[]` to fetch message number 3, header and body.
- `MOVE <sequence_set> <mailbox>` moves the specified messages to another mailbox
- `COPY <sequence_set> <data_item_name>` copies the specified messages to another mailbox
- `LOGOUT` logs out
