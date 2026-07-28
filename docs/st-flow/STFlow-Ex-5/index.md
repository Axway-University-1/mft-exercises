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

## Exercise 5 – Shared Folder Application

### About This Exercise

In this exercise, you will create a shared folder application that will allow two accounts to share content without being able to see each other's entire directory structure.

---

### Task 1: Create the Shared Folder Application

| Field | Value |
| --- | --- |
| Application Name | project1 |
| Application Type | Shared Folder |
| Folder | `/usrdata/shares/project1` |

1. Navigate to **Application → Application** in the administrative UI

2. Click *Add New*

3. Enter the information from the table above

   ![Shared folder application](images/image52.png)

4. Click *Create Application*

---

### Task 2: Create User Accounts

Create two accounts and subscribe them to the shared folder application.

**Account 1**

| Field | Value |
| --- | --- |
| Account Name | user1 |
| UID | 7001 |
| GID | 7000 |
| Change Home To | `/usrdata/NoBU/user1` |
| Allow login | Checked |
| Login Name | user1 |
| Password is stored locally | Checked |
| Password | axway |

**Account 2**

| Field | Value |
| --- | --- |
| Account Name | user2 |
| UID | 7001 |
| GID | 7000 |
| Change Home To | `/usrdata/NoBU/user2` |
| Allow login | Checked |
| Login Name | user2 |
| Password is stored locally | Checked |
| Password | axway |

1. Navigate to **Accounts → User Accounts**

2. For each account, click *New Account* and enter the information above

3. Click *Save*

4. Click the *Subscriptions* tab

5. Select *project1* from the *Subscribe to* drop-down field

6. Click *Subscribe…*

7. Enter `project1-share` in the *Subscription Folder* field

8. Click *Add*

> **NOTE:** Instead of creating the second account manually, you can duplicate it from the first (make sure you enable the second account after that, as *Duplicate* creates accounts in disabled mode).

---

### Task 3: Share a File

1. Connect to the end user web interface (`https://mft-env:8443`)

2. Log in as *user1*

3. Navigate into the *project1-share* folder

4. Click *Upload*

5. Select a file and click *Open*

6. Log out

7. Log in as *user2*

8. Navigate into the *project1-share* folder

9. Verify user2 sees the file user1 uploaded

10. Click on the file in the *Name* column to download

11. Verify the file was downloaded. Your tracking table should look something like this:

    ![Shared folder tracking](images/image53.png)

---
