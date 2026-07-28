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

## Exercise 6 – File Flow using Advanced Routing

### About This Exercise

In this exercise, you will simulate a real-world use case. Your internal application called *Manufacturing* will transmit files to SecureTransport, which will then be sent to a remote partner (your instructor's server).

---

### Task 1: Create a New Account called Manufacturing

| Field | Value |
| --- | --- |
| Account Name | Manufacturing |
| UID | 7001 |
| GID | 7000 |
| Home Directory | `/usrdata/NoBU/Manufacturing` |
| Password | axway |

---

### Task 2: Create a New Account called Instructor

| Field | Value |
| --- | --- |
| Account Name | Instructor |
| UID | 7001 |
| GID | 7000 |
| Home Directory | `/usrdata/NoBU/Instructor` |
| Password | axway |

---

### Task 3: Create a Transfer Site on the Instructor Account

Create a shareable transfer site with connectivity to the Instructor server that is accessible from ANY account or route on your SecureTransport instance.

| Field | Value |
| --- | --- |
| Transfer Protocol | SSH |
| Site Name | TS_SFTP_Instructor |
| Server | galaxy1 |
| Port | 8022 |
| Username | axway |
| Password | axway |
| Upload Folder | fromStockbroker (substitute your own node name) |
| Access Level | Public |

   ![Public transfer site](images/image54.png)

---

### Task 4: Create a Route Template

1. Navigate to **Routes → Route Templates** and click *+ Route Template*

   ![Route template](images/image55.png)

2. Create a new Route Template called `To Instructor`

3. Click *+ Add New Route* to add a new Simple route

4. Name: `SR_toInstructor` (leave all other fields at their default values)

   ![Simple route](images/image56.png)

5. Click *+ Step* to add a Rename step

6. Select *Rename* from the list of steps

7. Leave all values at default except for the *Output File Names*. Enter the following expression:

   ```text
   ${basename(transfer.target)}_${date("yyyy-MMM-dd_HH-mm")}
   ```

   This expression removes the extension from the filename and replaces it with an underscore followed by the current time. For example, `st.txt` becomes `st_2025-Oct-21_13-41`.

   ![Rename step](images/image57.png)

8. Press *Save Draft*

**Add a Send To Partner step:**

9. Click *+ Step* again and select *Send To Partner*

10. Select *Stop on Failure* in the *Flow* dropdown box

11. Specify an account: `Instructor`

12. Select the *TS_SFTP_Instructor* transfer site in *Account's Transfer Sites*

    ![Send to partner step](images/image58.png)

13. Click *Save Draft* to save the step

14. Click *Save Template*, then *Close*

---

### Task 5: Create an Advanced Routing Application

1. Click *Add New*

2. Provide a name – `AdvRouting` or anything you prefer

3. Select *Advanced Routing* from the dropdown

   ![Advanced routing application](images/image59.png)

4. Click *Create Application*

> The Advanced Routing application has no scenario-specific settings, so you will often have a single instance used by all subscriptions that use Advanced Routing.

---

### Task 6: Add a Route to the Manufacturing Account

1. Edit the Manufacturing account

2. Select the *Routes* tab

3. Use the dropdown to select the *To Instructor* Route Template and click *+ Assign Route*

   ![Assign route](images/image60.png)

4. Enter `PR To Instructor` as the Route Name

5. Click *Save*

6. Click on the *Subscriptions* tab and create a new Advanced Routing Subscription by selecting *AdvRouting* and *Subscribe…*

   ![Advanced routing subscription](images/image61.png)

7. Change the Subscription Folder name to `/toInstructor` and select the Route *PR To Instructor* from the Route dropdown

   ![Subscription route](images/image62.png)

8. Check the *On Success → Delete* option in Post Routing Settings

   ![Post routing settings](images/image63.png)

9. Save your subscription by clicking *Add*

---

### Task 7: Ask your instructor to Send you a file from the Manufacturing Application

1. Let your instructor know you are ready to receive a file, and tell them which server your system is (e.g. `agrifarm`, `stockbroker`)

2. Validate that you received the file and that its filename was transformed on transmission

   ![Received file](images/image64.png)

3. Verify that all route steps were successful by clicking on the filename of the inbound file

   ![Route steps success](images/image65.png)

---
