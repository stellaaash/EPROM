---
tags:
  - Windows
---
The **default authentication protocol for any recent version of Windows**.
# How it works
Users who log into a service using Kerberos are **assigned tickets**, which are basically session IDs that prove previous authentication.
## Usual Authentication Workflow
1. The user sends their username and a timestamp encrypted using a key derived from their password to the *Key Distribution Center or KDC*. This service is usually installed on the Domain Controller of the [[Active Directory]].
   The KDC will send back a *Ticket Granting Ticket (TGT)* which allows the now logged-in user to send additional requests for tickets to access specific services.
   It also sends back a *Session Key* which the user will use to generate the following requests.
   The TGT is encrypted using the `krbtgt` account's password hash.
   ![](https://tryhackme-images.s3.amazonaws.com/user-uploads/5ed5961c6276df568891c3ea/room-content/d36f5a024c20fb480cdae8cd09ddc09f.png)
2. When a user wants to connect to a service on the network (a share, website or database), they will use their TGT to ask the KDC for a *Ticket Granting Service (TGS)*.
   These are tickets that **allow connections only to the specific service they were created for**.
   To do so, the user sends the request along with their username and a timestamp encrypted with the Session Key, along with the TGT and the *Service Principal Name (SPN)*, which specifies the service and server name.
   Then, the KDC will send the user back a TGS along with a *Service Session Key*, which the user can now use to authenticate to the desired service.
   The TGS is encrypted using a key derived from the *Service Owner Hash*. The Service Owner is the user or machine account that the service runs under.
   The TGS contains a copy of the Service Session Key on its encrypted contents so that the Service Owner can access it by decrypting the TGS.
   ![](https://tryhackme-images.s3.amazonaws.com/user-uploads/5ed5961c6276df568891c3ea/room-content/84504666e78373c613d3e05d176282dc.png)
3. Finally, the TGS can then be sent to the desired service to authenticate and establish a connection.
   The service will use its configured account's password hash to decrypt the TGS and validate the Service Session Key.
   ![](https://tryhackme-images.s3.amazonaws.com/user-uploads/5ed5961c6276df568891c3ea/room-content/8fbf08d03459c1b792f3b6efa4d7f285.png)