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

## Exercise 9 – Compression and Subscription Triggering

### About This Exercise

The Human Resources department wishes to send a single zip file to their partner each day. The HR department will initiate the final transmission by uploading a file called `trigger.me`. Any file uploaded by HR that does NOT end with `.txt` should NOT be part of the archive and should be placed into another directory for analysis.

---

### Task 1: Create an HR account

1. Create an account with the name `HR` and password `axway`

   ![HR account](images/image81.png)

2. Create a New Route Template called `HR Outbound Processing`

3. Add a Simple Route with name `SR_Compress`

4. Add a compress step filtering for files with a filename pattern of `*.txt`

5. Create a Single Archive called `HR.zip`

   ![Single archive](images/image82.png)

6. Add the *Send to Partner* Step

   ![Send to partner](images/image83.png)

7. Make sure that the step processes only the zip files (via a file name condition or via processing only files coming from the previous step)

8. Ensure that you check *Delete Files after Step is complete*

   ![Delete files after step](images/image84.png)

**Add a Publish to Account Step:**

9. This step sends any files OTHER than the zip file to a directory called UNKNOWN underneath the home folder of the account

   ![Publish to account](images/image85.png)

> **Hint:** Click the pencil next to *Account* to add an expression instead of a name. `${account.name}` gives you the name of the account currently using this route.

10. The result should look like this:

    ![Route result](images/image86.png)

11. Save everything you created.

---

### Task 2: On the HR account create a route

1. Assign the route template to the HR account

   ![Assign route](images/image87.png)

2. Save the Route with name `PR_to_Partner`

   ![Save route](images/image88.png)

---

### Task 3: On the HR account create an Advanced Routing Subscription

| Field | Value |
| --- | --- |
| Subscription Folder | `/toPartner` |
| Route | PR_to_Partner |

1. Create the subscription

   ![Advanced routing subscription](images/image89.png)

2. Check *Delete on Success* to clean the folder after the file is successfully sent

   ![Delete on success](images/image90.png)

3. Check *Trigger processing of files based upon condition*

   ![Trigger processing](images/image91.png)

The trigger condition can be written in two ways:

   ```text
   ${stenv.target.matches('trigger.*')?1:0}
   ```

   or

   ```text
   ${stenv['target'].matches('trigger.*')?1:0}
   ```

> If you click the *?* button, you will see preset values you can modify to save some typing.

---

### Task 4: Load the Subscription Directory with Files

You could ask your instructor to do this, or log into the HR account via the Web Client and upload your own files followed by a trigger file. Files are provided under `STSOURCE/EX9`. Make sure there are at least a few files with a `.txt` extension.

1. Validate that nothing happens until the trigger file `trigger.me` is uploaded

   ![Trigger validation](images/image92.png)

---

