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

## Exercise 2 – Account Creation

### About This Exercise

We'll introduce you to the training environment and then get you started by creating your first account, along with your first file transfer.

---

### Task 1: Connect to SecureTransport

1. Open a browser on your lab server

2. Navigate to the admin GUI at `https://mft-env:8444`

   ![SecureTransport admin login](images/image13.png)

3. In the *User ID* and *Password* fields enter `admin`

> **NOTE:** If you took the Basic class and kept your server, use the password you changed the admin password to.

4. Click the *Sign in* button

---

### Task 2: Expanding and Shrinking the Left-Hand Navigational Menu

In this task, you will shrink and expand the left-hand navigational menu icons to reveal the textual representation of the icon.

1. Connect to the SecureTransport administration UI

2. Click on the **<** symbol at the bottom of the left-hand navigational menu

   ![Navigation menu collapsed](images/image14.png)

Hovering over any of the menus while they are not expanded will show you a tooltip with the name of the menu.

---

### Task 3: Create a New User Account

In this task, you will create a SecureTransport user.

> **NOTE:** The table below assumes you are student `01`. Substitute your own number where appropriate. Please name your account **John** as shown below. If you use a different name, remember it and use it any time the instructions in later exercises refer back to this account.

| Field | Value |
| --- | --- |
| Account Name | John |
| Email Contact | student01@demo.axway.com |
| Account Type | Unspecified |
| HTML Template | Default HTML Template |
| Route Mode | Reject |
| UID | 7001 |
| GID | 7000 |
| Change Home To (first field) | `/usrdata/NoBU` |
| Change Home To (second field) | John |
| Allow this account to login to SecureTransport Server | Checked |
| Login Name | John |
| Password is stored locally | Checked |
| New Password | axway |
| Re-enter Password | axway |

Add the following attributes (click *Add Attribute* for each, then click the checkmark to save):

| Attribute | Value |
| --- | --- |
| ownerAccountEmail | student101@demo.axway.com |
| supportAccountEmail | student201@demo.axway.com |

1. Connect to the SecureTransport administration UI at `https://mft-env:8444`

2. Navigate to **Accounts → User Accounts**

3. Click *New Account*

   ![New account](images/image15.png)

4. Enter the information from the table above into the appropriate fields

   ![Account attributes](images/image16.png)

5. Click *Save* (make sure you save each additional attribute separately by clicking the checkmark next to the attribute)

6. Click *Close*

---

### Task 4: Verify the Account was Added

1. Connect to the SecureTransport administration UI

2. Navigate to **Accounts → User Accounts**

3. Enter `John` in the *Search* field

   ![Search account](images/image17.png)

4. Click *Search*. You should see the following:

   ![Search results](images/image18.png)

5. Click on *John* in the *Account Name* field to open the account summary

   ![Account summary](images/image19.png)

6. Click *Edit Account Settings* to open the account in edit mode

7. Verify the information entered

8. Make an entry in Notes:

   ```text
   Created in Training Lab
   ```

9. Click *Save* and *Close*. You should now see the note in the account Notes field.

   ![Account notes](images/image20.png)

---

### Task 5: Transfer a File via the Web Browser

In this task, you will connect to your SecureTransport server as the user John, and upload a file using the HTTPS protocol.

1. Open your web browser

2. Navigate to `https://mft-env:8443`

3. Enter `John` as the User ID

4. Enter `axway` as the Password

5. Click *Sign In*

6. Click *Upload* and select a file to upload (any file will do)

   ![Upload file](images/image21.png)

7. Click *Open* on your selected file. The file should be successfully uploaded to your home folder.

   ![File uploaded](images/image22.png)

8. Click on the drop-down arrow next to John's name in the upper right-hand corner

9. Select *Logout*

---

### Task 6: Examine File Tracking

In this task, you will use SecureTransport's file tracking log to verify your file was uploaded successfully.

1. Connect to the SecureTransport administration UI as admin

2. Navigate to **Operations → File Tracking**

3. Verify you see an entry for the file you just uploaded

   ![File tracking](images/image23.png)

The green *Processed* icon indicates the file transfer was successful. Clicking on the filename will bring up detailed log information about the transfer.

   ![File tracking detail](images/image24.png)

The file we just uploaded was placed in the user's home directory. In the next exercise, we will create an outbound flow which processes the received file.

---

