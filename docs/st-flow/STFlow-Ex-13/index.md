---
layout: default
title: SecureTransport File Flows
---

# Axway University
# SecureTransport File Flows



| Workbook Version | 1.8 |
| ---- | ---- |
| Issued | July 2026 |
| ST Server Updated | May 2026 |
| Written by | Annie Yotova |

Welcome to the SecureTransport File Flows Lab! In this hands-on workbook, you will learn how to build, manage, and troubleshoot SecureTransport file transfer flows using user accounts, subscriptions, transfer sites, advanced routing, PGP encryption, shared folders, compression, and adhoc transfers.



---

## Exercise 13 – Enroll Unlicensed

### About This Exercise

We'll modify the previous use case to force a registration in ST for the user before they can download the file, so we can track who downloads the file.

---

### Task 1: Modify the Transfer Site used in EX12

1. Change the delivery method as shown

   ![Delivery method](images/image136.png)

---

### Task 2: Upload another file

1. Note that this time, the email recipient receives 2 emails

   ![Two emails](images/image137.png)

One email is an enrolment email. Click this first to create the temporary account.

> If you do not receive the emails, check your server logs. Is there a missing configuration? How will the server know how to enroll the user (what home folder to use)?

---

### Task 3: Create an account template to be used for the onboarding

Create an account template that will be used during enrollment.

---

### Task 4: Send a file again and check your mailbox again

1. You should now see two emails. Click on the enrolment one:

   ![Enrolment email](images/image138.png)

2. Login using the credentials supplied

3. The system will ask you to change your password immediately

4. After a successful password change, login again

   ![Login after password change](images/image139.png)

5. Click on *Mailbox* and then *Inbox*

   ![Mailbox inbox](images/image140.png)

6. Download the file

   ![Download file](images/image141.png)

> There is also an option to reply to the sender (the EX12 account) to let them know you received the file.

---

### Task 5: Check the Unlicensed User Accounts

1. Via the Admin UI you can control the unlicensed accounts that are created

   ![Unlicensed accounts](images/image142.png)

---

## End of Workbook


