---
title: Computing Concepts & Servers
teaching: 20
exercises: 10
---

:::::::::::::::::::::::::::::::::::::::::::::: questions

- Why do we use a remote server for microbial genomics?
- How is a server different from my laptop?
- How will I connect to and work on the workshop server?

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: objectives

- Describe the difference between local and remote computing.
- Identify the main hardware resources on a server (CPU, RAM, storage).
- Interpret the basic information shown when you log in to a Linux server.
- Connect to the workshop server using `ssh` or a terminal program.

::::::::::::::::::::::::::::::::::::::::::::::::::

> This episode is adapted from the Data Carpentry *Introduction to Cloud Computing
> for Genomics* and *Introduction to the Command Line for Genomics* lessons.

## Local vs remote computing

Most people are used to working on a **local computer**: a laptop or desktop they
can see and touch. For genomics, local machines are often not enough:

- Sequencing data files can be *many gigabytes* in size.
- Assembly and mapping tools can use *tens of gigabytes of RAM*.
- Analyses may run for *hours* or *days*.

A **server** (or *remote machine*) is just a more powerful computer that you log
into over the network. In this workshop, everyone will use the **same type of
remote Linux server**, pre-configured with the tools and data we need.

:::::::::::::::::::::::::::::::::::::::::::::: callout

## Vocabulary

- **Local machine** – the computer in front of you.
- **Remote server** – a computer in a different physical location that you
  connect to over the network.
- **Client** – the program on your local machine that talks to the server
  (Terminal, PuTTY, Windows Terminal, etc.).

::::::::::::::::::::::::::::::::::::::::::::::::::

## What resources does a server have?

Just like your laptop, a server has:

- **CPUs** (cores): do the actual calculations.
- **RAM** (memory): holds data and code *while* programs are running.
- **Disk storage**: where files live long-term (reads, assemblies, scripts).
- **Network connection**: lets you log in and transfer data.

Genomics workloads tend to be limited by **RAM** and **disk**. It is useful to
know that:

- If you run out of RAM, programs may crash or become very slow.
- If you run out of disk space, tools may refuse to run or fail with
  messages like *No space left on device*.

Your instructor or local sysadmin can tell you typical limits on the system you
are using.

## Connecting to the workshop server

Your instructor will provide:

- a **host name** (something like `genomics-server.university.edu`), and
- a **username** and **password** for your workshop account.

### macOS and Linux

On macOS and Linux, we use the built-in **Terminal** application and the
`ssh` command.

Open a terminal and type (replacing the pieces in angle brackets with the
values your instructor gives you):

```bash
ssh <username>@<server-address>
```

For example:

```bash
ssh learner01@genomics-server.university.edu
```

The first time you connect, you may see a security question about the
host key; answer `yes`. Then enter the password when prompted. Note that
the cursor will not move while you type the password – this is normal.

### Windows

On Windows, you can use a terminal program such as:

- **Windows Terminal** or **PowerShell** (on recent Windows 10/11),
- **PuTTY**, or
- **MobaXterm**.

Your instructor will demonstrate the recommended option for this workshop.
In all cases you will enter the **host name**, **username**, and **password**
that were provided.

## First look at the shell prompt

After you log in, you will see a message of the day followed by a line
that ends with a **prompt**, often something like:

```bash
learner01@genomics-server:~$
```

This usually shows:

- your **username**,
- the **server name**, and
- your current location in the filesystem (`~` means your home directory).

Everything you type from now on will be interpreted as **commands** to the
server, not your local machine.

Try the following commands to verify where you are:

```bash
whoami
hostname
pwd
```

- `whoami` prints your username on the remote server.
- `hostname` prints the name of the computer you are logged into.
- `pwd` prints the present working directory (your current folder).

:::::::::::::::::::::::::::::::::::::::::::::: challenge

## Exercise: Local or remote?

With a partner, decide whether each of the following is running on your **local
machine** or the **remote server**:

1. The browser window showing these lesson pages.
2. The terminal or SSH client you are using.
3. The `whoami` and `pwd` commands you just ran.
4. The FastQC and SPAdes runs we will do later.

Discuss why it matters where each thing is happening.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: keypoints

## Key Points

- We use a **remote server** for genomics because it has more CPU, RAM, and
  storage than a typical laptop.
- You connect to the server using an **SSH client** (Terminal, PuTTY,
  MobaXterm, etc.).
- After logging in, you type commands at a **shell prompt** that is running on
  the **remote** machine.
- Simple commands like `whoami`, `hostname`, and `pwd` help you confirm where
  you are and who you are logged in as.

::::::::::::::::::::::::::::::::::::::::::::::::::
