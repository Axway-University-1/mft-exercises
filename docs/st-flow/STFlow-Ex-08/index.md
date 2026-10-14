---
layout: default
title: SecureTransport File Flows
---

# Axway University
# SecureTransport File Flows


| ST Update | May 2026 |
| ---- | ---- |
| Exercise Update | October 2026 |


---

## Exercise 8 – Conditional Routing 2

### About This Exercise

The Manufacturing application owner does not have any requests for changes but in reviewing your setup, you realized that you did not reuse the Send To Partner step in your prevuous template. Let's optimize the setup so if you need to change the Send To Partner parameters, you do not need to do that in two different places. 

### High Level Solution

Editing route templates can be dangerous - you can see how many composite route packages use them but you do not know if anyone else plans to use it. So we will create a new template route for this exercise. Creating a new template route will also require a new composite route package and as we do not want the client to change the way they use the application, we will reuse their subscription and just point it to the new composite route package. 

---

### Task 1: Create a New Route Template

1. Give your Route Template a name such as `Ex8 – Compress`.

2. Add a New Route named `SR_Ex8`. Leave the default setting of "Always execute this route".

3. Add a Compress Step

4. Select *Stop on failure* in the *Flow* checkbox

5. In the *Current Filter* radio boxes field, select *Wildcard Pattern* and specify `*.txt` in the *Filter Pattern* field. The compress step will now only execute when a file pattern of `*.txt` is received.

   ![Wildcard filter](../images/image153.png)

6. Uncheck the *Compress all files into a single archive* checkbox. 

7. Press "Save Draft"

8. Add a *Send to Partner* Step

9. Select *Stop on failure* in the *Flow* checkbox

10. Switch the *Files to process* radio box to *All available files*

   ![Files to process](../images/image155.png)

11. "Save Draft", "Save Template", and "Close"

---

### Task 2: Create a New Route Package in the Manufacturing account

1. Create the route package with the name `PR Ex8 Compress` in the account selecting the "Ex8 – Compress" as the template. Don't forget to press "Save".

   ![Route package](../images/image157.png)


---

### Task 3: Modify the Subscription to point to the new Route

1. Modify the Manufacturing Account's subscription to point to the new route package

   ![Modify subscription](../images/image159.png)

---

### Task 4: Transfer files

1. Ask your instructor to send some more files or upload your own files in the Manufacturing account's /toInstructor folder. Then check the File Tracking table to see the results.

   ![Transfer files](../images/image161.png)

> Note how the end result is the same as with the previous exercise. If the files not ending in `.txt` were not sent, check that you changed *Files to process* in your Send To Partner step.

---

