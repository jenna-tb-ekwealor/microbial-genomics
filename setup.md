---
title: Getting Set Up for this Workshop
---

### Connect to the Server

In this workshop, you will run commands and analysis tools on a **remote Linux
server** that your instructors have prepared for you. This server already has
all required software installed:

- FastQC  
- fastp  
- SPAdes  
- Prokka  
- seqkit (optional utilities)

Your instructors will provide:

- the **server address** (e.g., `server.address.edu`)
- your **username**
- your **password**

You do *not* need to create an account, launch cloud instances, or configure AWS.
Everything you need is already prepared for you.

---

### Connecting to the Server

#### macOS and Linux Users

1. Open the **Terminal** application.
2. Connect using:

   ```bash
   ssh USERNAME@SERVER_ADDRESS
   ```

   Example (your values will differ):
   ```bash
   ssh workshopuser@server.address.edu
   ```

3. When asked about host authenticity, type:

   ```
   yes
   ```

4. Enter your password when prompted.

You are now logged in. Verify with:

```bash
whoami
pwd
```

---

#### Windows Users (Using PuTTY)

1. Install PuTTY: https://www.putty.org
2. Open PuTTY.
3. In **Host Name**, enter the server address (e.g., `server.address.edu`).
4. Click **Open**.
5. Log in using the username and password provided by instructors.

Verify login with:

```
whoami
pwd
```

---

### Testing Your Setup

Once logged in:

```bash
pwd              # shows your working directory
ls               # lists files
mkdir testdir    # make a directory
cd testdir       # move into it
```

If these commands run without error, your connection is successful.

---

### Troubleshooting

:::::::::::::::::::::::::::::::::::::::::: callout

#### Common Issues

- **Connection timed out**  
  → Double-check server address and your wifi connection.

- **Permission denied**  
  → Username or password is incorrect. Re-enter carefully.

- **Host authenticity warning**  
  → Type `yes` — this is expected the first time you connect.

- **Terminal freezes after password**  
  → Try typing password manually instead of pasting.

If none of these work, notify your instructor.

::::::::::::::::::::::::::::::::::::::::::::::::::

---

### You’re Ready!

Once connected, you will be able to follow all workshop episodes directly on the server.
Proceed to the first lesson: [**Computing Concepts & Servers**](01-why-cloud-computing.html).

