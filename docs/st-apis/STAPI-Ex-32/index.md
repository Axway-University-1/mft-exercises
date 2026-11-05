---
layout: default
title: SecureTransport APIs
---

# Axway University
# SecureTransport APIs

| ST Update | January 2026 |
| ---- | ---- |
| Exercise Update | April 2026 |

---

## Exercise 32 – Certificate Based Authentication and /Events

### About This Exercise

In this exercise, you will use certificate-based authentication rather than Basic Authentication. Certificate-based authentication is much more secure, so it is recommended for production usage or anywhere security is more of a concern.

The events API was added to SecureTransport in late 2022 and is a great way of determining the load on your system. Prior to this API, the only way of seeing the current event queue was to query the database itself.

---

### Task 1: Import the Trusted CA

We have generated a certificate chain that will be used to authenticate the APIs.

![Certificate chain](../images/image029.png)

The root and intermediate CAs have been saved in PEM format as file `STSOURCE/EX32/ST_Basics_Intermediate.pem`

1. In the ST Admin UI, go to *Certificates > Trusted CAs* and select **Import**

2. Provide an alias of `EX32` and select the above file

   ![Import trusted CA](../images/image031.png)

---

### Task 2: Enable Certificate Based Authentication for Administrators

1. Configure the Administrator login options as shown below

   ![Administrator login options](../images/image033.png)

> **NOTE:** Only enable the Root CA Certificate Authority as shown.

---

### Task 3: Add the Certificate Details to the Admin Account

1. The client certificate looks like this:

   ![Client certificate details](../images/image035.png)

   You could also see this via:

   ```text
   openssl x509 -in ST_Basics_Client.crt -text
   ```

2. Modify your admin account's *Certificate DN* field to contain:

   ```text
   CN=ST Basics Client,OU=Axway University,O=Axway,C=US
   ```

   ![Administrator certificate DN](../images/image037.png)

> **NOTE:** We are using the **APIadmin** account for our APIs.

---

### Task 4: Run the /events API

1. Issue the get events API:

   ```text
   ./stGetEvents.sh
   ```

2. Examine the script to verify that it is using certificate-based authentication

3. On an idle system, you should see a response as below, indicating there are no events active on the TM event queue:

   ```json
   { "resultSet" : { "returnCount" : 0,
                     "totalCount" : 0 },
     "result" : [ ]
   }
   ```

---

### Task 5: Create a Flow in SecureTransport

The idea here is to put sufficient load on the system so that there are events in progress. Either create a flow yourself that can be used to upload a large file and transmit it somewhere, or use the prebuilt account.

1. Run the following to construct an account called EX32 with a publish-to-account flow in it:

   ```text
   python3 stBuildEX32Account.py
   ```

   You can examine the JSON embedded within the code to determine the login credentials to use, and to see how the account was built using APIs.

2. Upload a large file to your test account. While the upload is in progress, run the `stGetEvents.sh` script again.

3. Once the advanced route is triggered, you should see something like:

   ![Events API output](../images/image039.png)

---