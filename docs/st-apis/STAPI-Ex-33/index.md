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

## Exercise 33 – Compare System Configs

### About This Exercise

In this exercise, you will emulate something you should be doing on your systems.

You will take a baseline of all the current system configuration values. The script saves these values as a file. Subsequent runs of the script compare the running system to the values in the baseline, and any differences are flagged.

This process should take place on a regular basis, especially after applying SecureTransport patches where default values may be changed.

---

### Task 1: Examine the Script

In `~/STSOURCE/EX33`, the Python script `stConfigScan.py` uses the `/configurations/options` API (using API windowing!) to retrieve all current configuration settings.

---

### Task 2: Create your Baseline

1. Run the script:

   ```text
   python3 stConfigScan.py MAKEBASELINE
   ```

   This creates a Python *pickle* file called `stConfig-10.129.61.87.baseline`

---

### Task 3: Change one of the System Parameters

1. Using the Admin UI, search for all *folder* parameters in the *Server Configuration*

   ![Server Configuration search](../images/image041.png)

2. Change `FolderMonitor.pollInterval` from the default of 5 seconds to a much more reasonable value of `120`

3. Run the Python script again using the argument `COMPAREBASELINE`:

   ```text
   python3 stConfigScan.py COMPAREBASELINE
   ```

   ![Compare baseline output](../images/image043.png)

4. You should see something like the above, showing that the program has detected the change

> **NOTE:** This is very useful after any ST patch or upgrade in particular, as new parameters are often added or values changed.

---