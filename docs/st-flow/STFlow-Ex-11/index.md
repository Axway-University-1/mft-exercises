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

## Exercise 11 – PGP

### About This Exercise

In this exercise, you will practice using PGP Encryption and Decryption within Advanced Routing flows. Your partner (your instructor) needs to receive PGP-encrypted files. You will transmit an Order file, and in turn receive a PGP-encrypted Invoice file.

---

### Task 1: Build an account

| Field | Value |
| --- | --- |
| Account Name | EX11PGP |
| UID | 7001 |
| GID | 7000 |
| Home Directory | `/usrdata/NoBU` |
| Password | axway |

---

### Task 2: Create a receiving subscription

1. On the `EX11PGP` account, create a receiving subscription folder called `/partnersPGPKeyIn`

2. Use the Basic application we created earlier

3. The subscription will not process the file – you are creating it so that ST can create the folder for the partner to send you their key

---

### Task 3: Ask your instructor to transmit his/her PGP public key to you

Download the file to your training server, or use the tracking table to discover where it is on the file system.

---

### Task 4: Import your Partner's Public PGP key

1. Select the EX11PGP account, go to *Certificates* and select *Partner Certificates*

   ![Partner certificates](images/image106.png)

2. Select *Import…*

3. Click *PGP key*

4. Provide an alias – i.e. `Instructor Public PGP Key`

   ![Import PGP key](images/image107.png)

5. Navigate to the downloaded file and press *Import*. If successful, you should see the imported key.

   ![Key imported](images/image108.png)

> **NOTE:** If you want the key listed in the dropdown in the encryption step, change the Access level to public and save.

   ![Public key access](images/image109.png)

---

### Task 5: Modify the Instructor's Transfer Site

1. Edit the Transfer site and check the *Allow Upload Folder Overwrite* box

2. Change the upload folder to the following expression:

   ```text
   ${stenv.subscription_attr_uservars_uploadfolder}
   ```

   ![Upload folder expression](images/image110.png)

3. Change the username to `ex11`; the password is again `axway`

   ![Username change](images/image111.png)

> Alternatively, you can create a new site as described above.

---

### Task 6: Create an 'Empty' Route Template if you do not have one

A route can also be specified on a per-account basis, so we'll complete this exercise using the Package Route on the EX11PGP account.

---

### Task 7: Create the EX11PGP account Package route for Encryption

1. Assign the empty template

   ![Encryption package route](images/image112.png)

2. Call your package route `PR_ENCRYPT`

3. Create a new local simple route called `SR_ENCRYPT`

4. Add the Encrypt step

   ![Encrypt step](images/image113.png)

5. For this exercise, use *Encrypt Only*

   ![Encrypt only](images/image114.png)

6. Add a *Send to Partner* Step

7. Select the Instructor account and the `TS_SFTP_Instructor` Transfer site

8. Check the *Overwrite Upload Folder* box and enter:

   ```text
   EncryptedFromStockbroker
   ```

   (Replace *Stockbroker* with your server name, first letter capitalized)

   ![Overwrite upload folder](images/image115.png)

9. Create the subscription (using the Advanced Routing application) with a folder name like `/EncryptandSendToInstructor`

10. Select your Package route

    ![Encryption subscription](images/image116.png)

11. Set the On Success Post Routing Action to *move* to:

    ```text
    /archive/${stenv.target}
    ```

    ![Post routing move](images/image117.png)

> Don't send any files yet – we'll build the rest of the scenario first.

---

### Task 8: Create your own Private PGP key

1. Click *Generate* having selected the *Private Certificates* tab

   ![Generate private key](images/image118.png)

2. Create an RSA PGP certificate of 4096 bytes. Substitute your server name and student number for the email.

   ![Private key details](images/image119.png)

3. Export your PGP public key by clicking the Alias in the list of certificates

   ![Export public key](images/image120.png)

4. Select *Export*. Do NOT select *Export private key*

   ![Export options](images/image121.png)

Your key will be downloaded as `xxxxxxxx.asc`.

---

### Task 9: Create a Package Route to Transmit your PGP key

1. Select the Empty Route Template to create a new Route in the account

   ![Send key route](images/image122.png)

2. Call your package Route `PR_sendKey`

3. Add a Simple route `SR_SendKey`

4. Overwrite the upload folder to be `/KeyFromStockbroker` (replace *Stockbroker* with your server name)

   ![Key upload folder](images/image123.png)

5. Create an Advanced Routing subscription with folder `/KeyToInstructor` and select the Route

   ![Key subscription](images/image124.png)

---

### Task 10: Send your PGP public key to your instructor

1. Use the web client to upload your Public PGP key to the `/KeyToInstructor` folder

2. Let your instructor know that you sent them your PGP public key

   ![Notify instructor](images/image125.png)

---

### Task 11: Build a Decryption Package Route

1. Using the Empty template, create a package route in the `EX11PGP` account

   ![Decrypt package route](images/image126.png)

2. Call it `PR_Decrypt`

3. Add an `SR_decrypt` simple route

4. Add a PGP Decrypt step (encryption only, no signature)

5. Add a *Publish to Account* step to put the file in a folder once decrypted

   ![Decrypt publish](images/image127.png)

---

### Task 12: Create the Subscription

1. Create an advanced routing subscription with folder `/EncryptedFromInstructor`

2. Link to your Package Route `PR_Decrypt`

   ![Decrypt subscription](images/image128.png)

---

### Task 13: Now send a file

1. Validate that the file you received is the same as the file you transmitted.

Remember that you archived the outgoing file in `/EncryptandSendtoInstructor/archive` and moved the decrypted version to `/Decrypted`.

---

### Task 14: Optional Task

For bonus points – send the decrypted incoming file to a folder underneath another account.

---
