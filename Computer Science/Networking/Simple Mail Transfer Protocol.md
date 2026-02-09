---
tags:
port: "25"
---
The Simple Mail Transfer Protocol is a standard internet communication protocol **for electronic mail transmission**.
Mail servers and [[Mail Transfer Agent]]s use SMTP to send and receive mail messages.
Users use clients that typically use SMTP **only for sending messages** to a mail server, which then relays them appropriately.
For retrieving messages, on the other hand, [[Internet Message Access Protocol]] is often used, or its older counterpart the [[Post Office Protocol]].
# How it works
Here is a rough overview of what happens when transferring an email to a SMTP server:
1. `HELO` or `EHLO` initiates a SMTP session
2. `MAIL FROM` specifies the sender's email address
3. `RCPT TO` specifies the recipient's email address
4. `DATA` indicates that the client will begin sending the contents of the email message
5. `.` is sent on a line by itself to indicate the end of the email message
