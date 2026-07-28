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

## Exercise 4 – Server Initiated Transfers

### About This Exercise

Now we'll examine the use case whereby SecureTransport will initiate the connection to the remote server and pull files based upon a schedule. We'll re-use the John account, modifying it to make it a purely automated account by removing the user's ability to login.

---

### Task 1: Disable Logins on the John Account

1. Edit the John account

2. Uncheck the *Allow this account to login to SecureTransport Server* checkbox

   ![Disable login](images/image40.png)

3. Click *Save*

---

### Task 2: Modify the Instructor Transfer Site

1. Edit John's Instructor Transfer Site

2. In the *Download Folder* field, add `/toStockbroker` (substitute your own servername)

3. Add a file Download pattern of `*.ex4`

   ![Download pattern](images/image41.png)

4. Click *Save*

---

### Task 3: Create a Folder Monitor Transfer Site

This transfer site will be used to push files retrieved from your instructor's server to a folder on your own local system.

1. In the John account, select the *Transfer Sites* tab and then *Add New*

2. Change the transfer Protocol from AS2 to *Folder Monitor*

3. Call the site `FM_TMP`

4. In the mandatory *Download Folder* enter `/nofiles`

5. The download pattern should be *nothing* or a string that never matches a filename (we do not wish to use the folder monitor for pulling any files)

   ![Folder Monitor site](images/image42.png)

6. Enter `/tmp` in the upload directory

7. Click *Add* to save your Folder Monitor

---

### Task 4: Create a New Subscription

1. In the John account, select the *Subscription* tab

2. Subscribe to the *BasicApp*

3. Change the Subscription folder to be `/pulledFromInstructor`

4. Select the *Automatically retrieve files from* box and highlight the Instructor transfer site

   ![Automatic retrieval](images/image43.png)

5. Select *Configure* under the *Schedule* area

6. On the schedule pop-up, check *Schedule events on a recurring basis*

7. Enter `30 minutes` for the schedule

   ![Schedule configuration](images/image44.png)

> **NOTE:** If you select *Start now*, the scheduler will execute soon after you save the site. If you do not want that, set the start time in the future.

8. Save your schedule using *OK*

9. Enter `5 days` in the *Keep Pull history* box

   ![Keep pull history](images/image45.png)

10. Select *FM_TMP* as the destination for your files and select *Delete on Success* at the bottom of the screen

    ![Destination selection](images/image46.png)

11. Save your subscription. You should now have two subscriptions in your account.

    ![Two subscriptions](images/image47.png)

---

### Task 5: Manually Initiate the Server Pull

1. On John's *Subscription* tab, click the `/pulledFromInstructor` BasicApp Subscription to edit it

2. Click the *Retrieve Files Now* button to manually trigger the pull

   ![Retrieve files now](images/image48.png)

---

### Task 6: Validate the Pull is working

1. Check the File Tracker

   ![File tracker](images/image49.png)

If you see any issues or there are no file transfers, check the Server Log and use the transfer site's *List* and *Connectivity* options to troubleshoot.

---

### Task 7: Initiate the Pull again

1. Select the *Retrieve files now* button on the Subscription again and observe the tracking table

   Why are no files being pulled this time? Check the Server Log.

   ![Server log](images/image50.png)

2. On the *Subscription* tab of the John account, select the subscription by checking the checkbox in front of it, check the *Clear Pull History* option, and then click *Execute*

   ![Clear pull history](images/image51.png)

3. Confirm that you can pull the same file again now.

---
