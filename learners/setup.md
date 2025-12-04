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

Some additional software, detailed below, must be installed on your computer.

Please follow the instructions below to prepare your computer for the workshop:

- Required additional software + Option A
  **OR**
- Required additional software + Option B


---


## Required additional software

This lesson requires a working spreadsheet program.
If you don't have a spreadsheet program already, you can use LibreOffice.
It's a free, open source spreadsheet program.
Directions to install are included for each Windows, Mac OS X, and Linux systems below.
For Windows, you will also need to install either Git Bash, PuTTY, or the Ubuntu Subsystem.

:::::::::::::::: spoiler

## Windows

- Visit [the LibreOffice installation page](https://www.libreoffice.org/download/libreoffice-fresh/).
  The version for Windows should automatically be selected.
  Click Download Version X.X.X (whichever is the most recent version).
  You will go to a page that asks about a donation, but you don't need to make one.
  Your download should begin automatically.
- Once the installer is downloaded, double click on it and LibreOffice should install.
- Download the [Git for Windows installer](https://git-for-windows.github.io/).
  Run the installer and follow the steps below:
  - Click on "Next" four times (two times if you've previously installed Git).
    You don't need to change anything in the Information, location, components, and start menu screens.
  - **From the dropdown menu select "Use the Nano editor by default"
    (NOTE: you will need to scroll up to find it) and click on "Next".**
  - On the page that says "Adjusting the name of the initial branch in new repositories",
    ensure that "Let Git decide" is selected.
    This will ensure the highest level of compatibility for our lessons.
  - Ensure that "Git from the command line and also from 3rd-party software"
    is selected and click on "Next".
    (If you don't do this Git Bash will not work properly,
    requiring you to remove the Git Bash installation,
    re-run the installer and to select the
    "Git from the command line and also from 3rd-party software" option.)
  - Ensure that "Use the native Windows Secure Channel Library" is selected and click on "Next".
  - Ensure that "Checkout Windows-style, commit Unix-style line endings" is selected and click on "Next".
  - **Ensure that "Use Windows' default console window" is selected and click on "Next".**
  - Ensure that "Default (fast-forward or merge) is selected and click "Next"
  - Ensure that "Git Credential Manager Core" is selected and click on "Next".
  - Ensure that "Enable file system caching" is selected and click on "Next".
  - Click on "Install".
  - Click on "Finish".
  - Check the settings for you your "HOME" environment variable.
    - If your "HOME" environment variable is not set (or you don't know what this is):
    - Open command prompt (Open Start Menu then type `cmd` and press [Enter])
    - Type the following line into the command prompt window exactly as shown: `setx HOME "%USERPROFILE%"`
    - Press [Enter], you should see `SUCCESS: Specified value was saved.`
    - Quit command prompt by typing `exit` then pressing [Enter]
- An **alternative option** is to [install PuTTY](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html).
  For most newer computers, click on putty-64bit-X.XX-installer.msi to download the 64-bit version.
  If you have an older laptop, you may need to get the 32-bit version putty-X.XX-installer.msi.
  If you aren't sure whether you need the 64 or 32 bit version,
  you can [check your laptop version](https://support.microsoft.com/en-us/help/15056/windows-32-64-bit-faq).
  Once the installer is downloaded, double click on it, and PuTTY should install.
- **Another alternative option** is to use the Ubuntu Subsystem for Windows.
  This option is only available for Windows 10 - the Microsoft documentation provides
  [detailed instructions for installing Windows 10](https://docs.microsoft.com/en-us/windows/wsl/install-win10).

:::::::::::::::::::::::::

:::::::::::::::: spoiler

## Mac OS X

- Visit [the LibreOffice installation page](https://www.libreoffice.org/download/libreoffice-fresh/).
  The version for Mac should automatically be selected.
  Click Download Version X.X.X (whichever is the most recent version).
  You will go to a page that asks about a donation, but you don't need to make one.
  Your download should begin automatically.
- Once the installer is downloaded, double click on it and LibreOffice should install.

:::::::::::::::::::::::::

:::::::::::::::: spoiler

## Linux

- Visit [the LibreOffice installation page](https://www.libreoffice.org/download/libreoffice-fresh/).
  The version for Linux should automatically be selected.
  Click Download Version X.X.X (whichever is the most recent version).
  You will go to a page that asks about a donation, but you don't need to make one.
  Your download should begin automatically.
- Once the installer is downloaded, double click on it and LibreOffice should install.

:::::::::::::::::::::::::

## Option A (**Recommended**): Doing the lessons on the remote server

Instructors will provide a remote server option that includes software and data you will need for this workshop. 

## Option B: Doing the lessons on your local machine

While not recommended, it is possible to work through the lessons on your local machine (i.e. without using the remote server). To do this, you will need to install all of the software used in the workshop and obtain a copy of the dataset. 

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

