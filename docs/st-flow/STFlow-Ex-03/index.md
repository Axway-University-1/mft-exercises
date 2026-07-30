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

## Exercise 3 – Complete Outbound Flow

### About This Exercise

In the prior exercise, we simply uploaded a file to the John account. Now we'll add the other components needed to create a complete file flow – the file will be transmitted to another system upon its upload to ST.

---

### Task 1: Create the Basic Application

1. Connect to the SecureTransport administration UI as the admin

   ![Applications](./images/image045.png)

2. Navigate to *Application* and click on *Add New*

   ![Add new application](./images/image047.png)

3. Select *Basic Application* from the application Type drop down menu

4. Provide a name for your application i.e. `BasicApp`

5. Select *Create Application*

---

### Task 2: Add an SSH Transfer Site to John Account

Now, we will add the file transfer flow to the John account. We will still use the web browser to upload files, but it will now transmit the files using SFTP to your instructor's server.

1. Select the John account and click the *Transfer Sites* tab

   ![Transfer sites tab](./images/image049.png)

2. Click on *Add New*

3. Change the Transfer Protocol from AS2 to SSH

   ![Add new transfer site](./images/image051.png)

4. Configure the transfer site:

| Field | Value |
| --- | --- |
| Transfer Protocol | SSH |
| Site Name | Instructor |
| Server | galaxy1 |
| Port | 8022 |
| Upload Folder | fromStockbroker |
| User Name | axway |
| Password | axway (check the *use password* box) |

> **NOTE:** Use your **servername** as part of the upload folder – so if your server is `stockbroker`, make the upload folder `fromStockbroker` (use uppercase for the first letter of your servername).

5. Save your site using the *Add* button. The result should look like this:
   ![Add new transfer site](./images/image053.png)



---

### Task 3: Validate Connectivity to your Instructor's Server

1. Click the *Instructor* Transfer Site to open it up again

2. Click the *Test connection* button

   ![Test connection](./images/image056.png)

3. Verify that both connectivity AND authentication are correct; resolve any errors if required.

   ![Connectivity result](./images/image058.png)

4. Check the contents of the remote upload directory by clicking *List*

   ![List directory](./images/image060.png)

It is probably empty at this time.

---

### Task 4: Create a Subscription Folder

1. Select the *Subscriptions* tab

   ![Subscriptions tab](./images/image063.png)

2. Select *BasicApp* from the *Subscribe to* dropdown and click *Subscribe…*

3. Change *BasicApp* to something more meaningful – perhaps `toInstructor`

   ![Subscription folder](./images/image065.png)

4. Scroll down to the *For Files Sent to this Account…* section (the outbound settings)

5. Check the *Send Files Directly To* box and click on the Instructor Transfer Site

6. Check the *on Success Delete* option

   ![Outbound settings](./images/image067.png)

7. Save the subscription via *Add*

   ![Save subscription](./images/image069.png)

---

### Task 5: Upload a File

Any files received in the `toInstructor` folder will be transmitted to the remote server via SFTP – in this case, your instructor's server.

1. Open your web browser

2. Navigate to `https://mft-env:8443`

3. Enter `John` as the User ID

4. Enter `axway` as the Password

5. Click *Sign In*

6. Click the *toInstructor* folder

7. Upload a file (any file will do)

   ![Upload to folder](./images/image071.png)

Note that on success, the file is no longer visible in the upload folder.

8. Click on the *Uploads monitor* button – you will see your file transfer

   ![Uploads monitor](./images/image073.png)

9. Login to the admin GUI and check the File Tracking

   ![File tracking](./images/image075.png)

10. Open the Instructor Transfer Site attached to the John account and select *List* on the upload folder (fromStockbroker)

    ![List upload folder](./images/image077.png)

---

