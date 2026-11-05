---
layout: default
title: SecureTransport APIs
---

# Axway University
# SecureTransport APIs

| ST Update | January 2026 |
| ---- | ---- |
| Exercise Update | November 2026 |

---

## Exercise 35 – User APIs Part 2

### About This Exercise

In `~/STSOURCE/EX35`, you will see several shell scripts that, when executed in sequence, allow you to upload a file and then query the status of the file transfers.

You will be using session management. Remember that when you do a `POST /myself`, the ST server returns a `csrfToken` header which needs to be used subsequently.

---

1. Run the scripts in sequence:

   ```text
   ./1-stLogin.sh
   ./2-stGetFileOperationsId.sh
   ./3-stGetFileOperationsId.sh
   ./4-GetUploadStatus.sh
   ./5-stLogout.sh
   ```

---

