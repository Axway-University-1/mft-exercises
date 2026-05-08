# SecureTransport Basic Administration

---

**Axway University**  
**SecureTransport Installation – Rocky Linux 9**  
Version 1.8 | Issued: April 2026 | *Internal / External*

---

*Copyright © Axway 2026. All Rights Reserved.*

---

## Document History

| Version | Date | Update Origin | Written by | Verified by |
| --- | --- | --- | --- | --- |
| 1.8 | April 2026 | Software and environment updates. Current as of 202601 release | Annie Yotova |  |
| 1.7 | January 2026 | Software and environment updates. Current as of 202509 release. Numbering to match the pptx versioning | Annie Yotova |  |
| 1.5 | April 2025 | Software and environment updates. Current as of 202502 release | Annie Yotova |  |


---

## Table of Contents

- [Exercise 1 – Introduction to the Environment](#exercise-1--introduction-to-the-environment)
  - [Task 1: Access the Training Environment](#task-1-access-the-training-environment)
  - [Task 2: Uninstall SecureTransport](#task-2-uninstall-securetransport)
- [Exercise 2 – Install SecureTransport](#exercise-2--install-securetransport)
  - [Task 1: Unzip the Installation Kit](#task-1-unzip-the-installation-kit)
  - [Task 2: Begin the Core Server Installation](#task-2-begin-the-core-server-installation)
  - [Task 3: Post Installation Configuration](#task-3-post-installation-configuration)
  - [Task 4: Restart SecureTransport](#task-4-restart-securetransport)
  - [Task 5: Disable the Setup Account](#task-5-disable-the-setup-account)
  - [Task 6: Start the Protocol Daemons if they are not running](#task-6-start-the-protocol-daemons-if-they-are-not-running)
- [Exercise 3 – Size your JVMs](#exercise-3--size-your-jvms)
  - [Task 1: Determine Allocations](#task-1-determine-allocations)
  - [Task 2: STStartScriptsConfig](#task-2-ststartscriptsconfig)
  - [Task 3: Restart ST](#task-3-restart-st)
- [Exercise 4 – Administrator LDAP](#exercise-4--administrator-ldap)
  - [Task 1: Configure LDAP](#task-1-configure-ldap)
  - [Task 2: Create a new Administrator](#task-2-create-a-new-administrator)
  - [Task 3: Login as the new Administrator](#task-3-login-as-the-new-administrator)

---

## Exercise 1 – Introduction to the Environment

### About This Exercise

In this exercise, you will be introduced to the SecureTransport environment.

---

### Task 1: Access the Training Environment

**Know your own parameters.**

Each course attendee will have their own unique parameters for use within the labs. The lab will have green highlighting where you need to substitute your own values.

| Your Name | Student # | Server Name | Access Code | IP Address |
| --- | --- | --- | --- | --- |
| Johana | 00 | galaxy1 | 3989412300 | 10.0.245.71 |
| Damien | 01 | stockbroker | 3989412301 | 10.0.243.129 |
| Thierry | 02 | bigbank | 3989412302 | 10.0.244.124 |
| Franck | 03 | agrifarm | 3989412303 | 10.0.246.104 |
|  | 04 | tractorco |  | 10.0 |
|  | 05 | hospital |  | 10.0. |
|  | 06 | drugco |  | 10.0. |
|  | 07 | localgovt |  | 10.0. |
|  | 08 | federal |  | 10.0. |
|  | 09 | marsco |  | 10.0. |
|  | 10 | jupiter |  | 10.0. |
|  | 11 | catco |  | 10.0. |
|  | 12 | dogco |  | 10.0. |
|  | 13 | bearco |  | 10.0. |
|  | 14 | apple |  | 10.0. |
|  | 15 | orange |  | 10.0. |
|  | 16 | peach |  | 10.0. |
|  | 17 | banana |  | 10.0. |
|  | 18 | getty |  | 10.0. |

In this task, you will connect to the Axway/ReadyTech training environment and log into your training server.

1. Open a browser on your desktop

2. Navigate to `https://axway.instructorled.training`

   ![Training environment access](images/image3.png)

3. Enter the access code provided by your instructor and click *Continue*

4. When logging in for the first time, you will be presented with an access code activation dialog box. Enter your first and last name, check the consent box, and click **OK**.

   ![Access code activation](images/image4.png)

5. Once logged in, you will see the following:

   ![Training environment home screen](images/image5.png)

6. Click on *Lab* at the top of the screen. You should see this screen:

   ![Lab screen](images/image6.png)

7. Verify that *ReadyTech View (HTML)* is selected in the *Remote desktop* section. Click on **Connect to the lab** in the Remote desktop section

8. Enter `axway` in the *Login* and *Password* fields of the *Log in* dialog box

   ![Login](images/image7.png)

9. At this point you should have access to your lab server desktop

   ![Lab server desktop](images/image8.png)

> **NOTE:** Click on **Activities** at the top left corner at any time to bring this UI to the front. If there are open applications (such as Firefox, Filezilla and so on), you will see them here as well.

---

### Task 2: Uninstall SecureTransport

Your environment will contain a pre-installed version of SecureTransport.

Our objective will be to remove the already existing installation and install the current version of ST.

**Shutdown SecureTransport if it is already running:**

```bash
cd /opt/Axway/ST/SecureTransport/bin
./stop_all
ps -ef | grep Secure
```

There should be no processes besides the grep process itself:

![No running processes](images/image9.png)

**Uninstall SecureTransport:**

```bash
cd /opt/Axway/ST
./uninstall.sh -m console
```
![Uninstall script](images/image10.png)

Press **Enter** or `y` when prompted.

![Prompt during uninstall](images/image11.png)

> **NOTE:** Some versions of ST may throw a warning about missing SLF4J loggers. These warnings can be safely ignored.

If the summary or the status shows any errors, consult the `install.log` file.

![Uninstall completion screen](images/image12.png)

---

## Exercise 2 – Install SecureTransport

We have already performed all pre-installation checks as per the Installation manual.

There are a few versions of the installation kit in the folder `/home/axway/Installers/ST/Install` and the licences required for ST are in the folder `/home/axway/Installers/ST`. Your instructor will let you know which of the provided installers to use.

We'll be performing a **non-root installation** as this follows security best practices.

---

### Task 1: Unzip the Installation Kit

The name of your installation kit will vary as SecureTransport is released on a monthly basis.

Below is only an example (for January 2026) – your file may be named differently:

```bash
unzip SecureTransport_5.5-20260129_Install_linux-x86-64_BN3237.zip
```

---

### Task 2: Begin the Core Server Installation

1. **Run the setup command:**

   ```bash
   ./setup.sh -m console
   ```

   ![Installation](images/image13.png)

2. **Accept the license**

   > **NOTE:** The number of pages depends on the resolution and the size of your screen and window.

   ![Accept License](images/image14.png)

3. **Select the Installation Directory of the Installer Product**

   ```
   Type the option you want to modify: 2
   Type the directory name when prompted: /opt/Axway/ST
   ```

   ![Select Install Dir Prod](images/image15.png)

4. **Select Server or Edge** — select *Server* for this installation

   ![Select Modules](images/image16.png)

5. **Select the Installation Directory for SecureTransport** — choose the Default for the ST installation directory

   ![Select Install Dir ST](images/image17.png)

6. **Select the Database** — select *Embedded Database* for this exercise

   ![Select Database](images/image18.png)

7. **Installation type** — select *Standalone*

   ![Select Install Type](images/image19.png)

8. **Database settings**

   > **NOTE:** Password is mandatory and cannot be left as the default value. Select `2` and set the password.

   ![Select DB settings](images/image20.png)

9. **Configuration settings**

   Set `Cluster Auto-Register IP/FQDN` to `mft-env` (Select `5` to update the value).

   Follow the prompts to start the installation after that.

   ![Configuration settings](images/image21.png)

10. **Validate the admin interface is running:**

    ```bash
    netstat -an | grep 8444
    ```

    If you changed the Admin port in step 9, use the port you selected there instead of `8444`.

    ![Configuration settings](images/image23.png)

Your SecureTransport is now installed, and you can proceed with its configuration.

---

### Task 3: Post Installation Configuration

Your VM has a nodename of `mft-env`.

**Connect to the Admin GUI:**

In a browser, connect to the UI at:

```
https://mft-env:8444
```

> The certificate is not trusted so accept the risks that the browser mentions.

The special *setup* account will walk you through the process – username `setup`, password `setup`.

> **NOTE:** Changing the setup account's password is **mandatory** for security reasons so you will need to change the password before you can proceed.

> **NOTE:** The UIs may look slightly different if you are installing a different version. The below screenshots are for the September 2025 update of ST.

![Admin UI login](images/image24.png)

![Password reminder ](images/image25.png)

---

**Install the licenses**

Licenses can be found in `/home/axway/Installers/ST`

- **Method 1:** Copy and paste the contents of the files into the GUI and select **Update License** each time.
- **Method 2:** Using the command line and the file system directly – copy the license files to the SecureTransport configuration folder as below:

  ```bash
  cp filedrive.license /opt/Axway/ST/SecureTransport/conf
  cp st.license /opt/Axway/ST/SecureTransport/conf
  ```

![Update license ](images/image26.png)
---

**Create the Keystore Password**

Do not enter anything in the "Current password" field.

Ensure that you remember the password you have set! For this exercise, we recommend `Axway123`. However, any password can be used.

![Keystore password](images/image27.png)

On successful update, the server will show you a green notification on the screen and close the secondary window, returning you to the main page:

![Keystore password success main page](images/image28.png)

---

**Generate a new CA**

During installation, a temporary Certificate Authority (CA) is created. You can either import your own CA certificate from your organization (typically an intermediate certificate with signing attributes) or, for the purposes of this exercise, create a self-signed certificate by selecting ***Generate New Internal CA***. The original CA remains on the server under a new name, ensuring that all certificates signed by it remain valid.

Use the name of your VM – `mft-env` – as the common name.

Select **Generate**. The screen refreshes after the certificate is created and displays briefly a green success message, then closes the secondary window and returns you to the previous screen.

![Generate Internal CA](images/image29.png)
![Generate Internal CA window](images/image30.png)

Your internal CA should now look something like this:

![Internal CA view](images/image31.png)

---

**Generate Certificates**

Now we need to generate the required certificates. These will all be signed by the new CA.

First, the `admind` certificate. A temporary admind certificate was created at installation time. This certificate is valid for 30 days and was signed by the auto-generated CA. Now, we need to replace it. The admind certificate is the certificate used for the admin GUI you are now using via the browser and cannot be renamed.

> **NOTE:** Never delete the admind certificate.

![Existing admind certificate](images/image32.png)

Click on **Generate** and select *X.509 Certificate*:

![Generate X.509 certificate screen](images/image33.png)

This will open the screen for generating the new certificate:

![New certificate generation screen](images/image34.png)

You will be asked if you wish to overwrite the existing admind certificate – select **Overwrite**.

> **NOTE:** If you want to preserve the original certificate, export it before you generate the new one.

![New certificate generation screen](images/image35.png)

The screen refreshes after the certificate is created and displays briefly a green success message, then closes the secondary window and returns you to the previous screen which should look like this:

![Certificate list after admind generation](images/image36.png)

Repeat the above steps to generate the following certificates:

| Alias | Purpose |
| --- | --- |
| `mdn` | Creating the MDNs for all files transferred through the server |
| `streaming` | Securing the communication with any edges you may want to connect |
| `cluster` | Securing the cluster communication if installing more than one server |
| `ssh_server` | Used for the SSH server |
| `ssl_server` | Used for all SSL servers (you can also create separate certificates for each service or import externally signed certificates) |

The result should be something like this:

![Full certificate list](images/image37.png)

---

**Configure Protocol Daemons**

Now enable the protocol servers for the protocols we'll be using.

First let's enable HTTPS.

![Server control](images/image38.png)

Select the ellipsis next to the *"Http Default"* server, then select the **Settings** icon:

![HTTP Default server settings icon](images/image39.png)

This will open the following screen:

![HTTPS configuration screen](images/image40.png)

In the *"SSL Key Alias"* field in the *SSL Settings* section, select the `ssl_server` certificate we generated previously. This is what will be seen by user clients when they connect to the Web Client interface or the User API. Make sure you enable **HTTPS** and **HSTS**. If you enable HTTP, the listener will be started but you will need to do additional changes to allow your server to accept non-secure connections.

![HTTPS configuration screen continued](images/image41.png)

Similarly, enable the SFTP server.

In the *"SSH Key Alias"* field, select the `ssh_server` certificate that was created earlier and make sure you enable both **SFTP** and **SCP**. By default, some weak key exchange algorithms are enabled. You can disable them at this stage or later. If the daemon is already running, this change requires a restart.

---

### Task 4: Restart SecureTransport

Because multiple configuration changes were made, SecureTransport must be shut down completely and restarted.

Command line scripts are found under the `<installationDir>/bin` folder (if you installed in the folder specified in Task 2, your installation directory is `/opt/Axway/ST/SecureTransport`).

```bash
cd /opt/Axway/ST/SecureTransport/bin
./stop_all
```

Verify that all JVMs are stopped:

```bash
ps -ef | grep Secure
```

Now, start up SecureTransport:

```bash
./start_all
```

Verify that the admin is started:

```bash
netstat -an | grep 8444
```

---

### Task 5: Disable the Setup Account

We no longer need the setup account – so login as the normal Master Administrator:

| | |
| --- | --- |
| **URL** | `https://mft-env:8444` |
| **Username** | `admin` |
| **Password** | `admin` |

You will again be forced to change the default admin password. Once you do that, you will see the main dashboard of the server:

![Main dashboard](images/image42.png)

Navigate to **Accounts → Administrators**.

![Accounts > Administrators](images/image43.png)

You will see all the default accounts created at installation time.

Delete the **account** and **application** accounts. If you want to explore them instead, their passwords match their names. You can also change their passwords or lock them instead of removing them.

**Lock the setup account.**

> **NOTE:** Please leave the **dbsetup** account intact. You can change its password if you want to (the current password is **dbsetup**).

![Accounts > Administrators > Setup](images/image45.png)

---

### Task 6: Start the Protocol Daemons if they are not running

As you executed `start_all` earlier in Task 4, the protocol daemons should be already started. This exercise shows you how you can start them from the UI if necessary.

You can start the HTTPS daemon by clicking the top ellipsis menu next to *"HTTP Service"*.

![Server Control - HTTPS Daemon](images/image46.png)
![Server Control - HTTPS Start Daemon](images/image47.png)

You can start the SSH daemon in a similar manner.

Your Server Control Panel should now look like this:

![Server Control Panel with daemons running](images/image48.png)

---

## Exercise 3 – Size your JVMs

SecureTransport provides default settings to get you up and running during installation; however, these settings are not typically appropriate for larger systems.

---

### Task 1: Determine Allocations

Find out how much memory you are working with and determine how much can be used per daemon.

Issue the `top` command:

![top command output](images/image49.png)

The screenshot above shows that we have ~23Gb physical memory on this Server. Note that on some OS versions, the memory will be shown in KiB and not MiB.

The JVMs we are running are the **TM**, **ADMIN**, **SSHD**, **HTTPD**.

Remember also that we are running the Database server on the same server.

In the absence of any other information, let's leave 4Gb to the Operating System itself and 4Gb for the Database. That leaves us **15Gb** we can allocate to ST's Java processes.

| JVM | Allocation | Rationale |
| --- | --- | --- |
| Admin | 1Gb | Using APIs but only 3 administrators |
| TM | 3Gb | Main engine – needs plenty of room |
| SFTP | 3Gb | Main protocol, usage expected to increase |
| HTTP | 1Gb | Used much less frequently |

> **NOTE:** You do not need to allocate all your available memory but ST cannot use memory that has not been allocated.

![top command output](images/image49.png)

---

### Task 2: STStartScriptsConfig

Edit `STStartScriptsConfig`:

```bash
cd /opt/Axway/ST/SecureTransport/conf
vi STStartScriptsConfig
```

- Select `I` to begin editing
- Save by using `Esc` then `:wq!`

You can also use the text editor accessible through the applications line at the bottom of your screen (please refer to the top of the document for instructions). You can use a combination of **M** and **G** notations in the file.

> Note that ST comes out from a clean installation with memory values prepopulated and commented. The `TM_JAVA_OPTS` options are uncommented after a fresh install.

![Allocations](images/image50.png)

---

### Task 3: Restart ST

```bash
/opt/Axway/ST/SecureTransport/bin/stop_all
```

Verify that all processes have stopped:

```bash
ps -ef | grep Secure
```

```bash
/opt/Axway/ST/SecureTransport/bin/start_all
```

> **NOTE:** For complete tuning of your system, please consult the following Support article:
> https://support.axway.com/kb/191062/

---

## Exercise 4 – Administrator LDAP

---

### Task 1: Configure LDAP

Go to **Server Configuration** and find the parameter:

```
Plugins.Authentication.admin-ldap-authentication-plugin
```
![Server config authentication plugin](images/image51.png)
Add a name for your plugin profile (for example `Default`). Note that the parameter names shown in the table below are based on the profile name you specified. If you decide to use a different name, replace **Default** in the variable names with the profile name you selected.

| Parameter | Value |
| --- | --- |
| `Plugins.Authentication.admin-ldap-authentication-plugin.Default.ldapConnectionType` | `normal` |
| `Plugins.Authentication.admin-ldap-authentication-plugin.Default.ldapHost` | `axwaydemo.com` |
| `Plugins.Authentication.admin-ldap-authentication-plugin.Default.ldapServerName` | `axwaydemo.com` |
| `Plugins.Authentication.admin-ldap-authentication-plugin.Default.ldapPort` | `389` |
| `Plugins.Authentication.admin-ldap-authentication-plugin.Default.ldapServerVersion` | `3` |
| `Plugins.Authentication.admin-ldap-authentication-plugin.Default.ldapUseReferrals` | `true` |
| `Plugins.Authentication.admin-ldap-authentication-plugin.Default.ldapBindDN` | `cn=Administrator,dc=demo.axway,dc=com` |
| `Plugins.Authentication.admin-ldap-authentication-plugin.Default.ldapBaseDN` | `ou=users,dc=demo.axway,dc=com` |
| `Plugins.Authentication.admin-ldap-authentication-plugin.Default.ldapBindPassword` | `axway` |
| `Plugins.Authentication.admin-ldap-authentication-plugin.Default.ldapAuthenticationBindTyp` | `admin` |
| `Plugins.Authentication.admin-ldap-authentication-plugin.Default.ldapSearchFilter` | `sn=${authn.loginname}` |

Your LDAP server configuration is now complete. The next step is to enable the plugin.

Edit *Plugins.Authentication.Admin.Registry*:

- If the field is **empty**, change the value to `LDAP`
- If the field is **not empty**, add `LDAP` on a separate line at the end of the field.

> **Note:** You can also use a different name for your registry. This will change the variable names in the next steps.

In the newly shown fields (note that the names of the fields depend on the name you chose in the previous step so your fields may be different):

| Parameter | Value |
| --- | --- |
| `Plugins.Authentication.Admin.Registry.LDAP.enabled` | `true` |
| `Plugins.Authentication.Admin.Registry.LDAP.plugin` | `admin-ldap-authentication-plugin` |
| `Plugins.Authentication.Admin.Registry.LDAP.conf` | `Default` *(matching the value from the start of the exercise)* |

> **NOTE:** This configuration can also be done via the new Configuration Group settings in the Configuration page using the **Authentication.Plugins.Chain.Group** group.

---

### Task 2: Create a new Administrator

Select **New Administrator** and add *Sebastian* as a Master Administrator.

![New administrator](images/image52.png)
![Sebastian](images/image53.png)

Save the changes with the **Password is stored locally** option **unchecked**.

---

### Task 3: Login as the new Administrator

If all is correctly configured – you should now be able to log in as administrator:

| | |
| --- | --- |
| **Username** | `Sebastian` |
| **Password** | `sebastian` |

Look at the **Server Log** if you get login failures to help find which parameter has been incorrectly specified – or whether the LDAP server itself has issues.