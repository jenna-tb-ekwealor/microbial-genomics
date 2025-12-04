---
title: Introducing the Shell
teaching: 25
exercises: 15
---

:::::::::::::::::::::::::::::::::::::::::::::: questions

- What is the Unix shell?
- How do I run commands on the workshop server?
- How do I navigate files and folders using basic Unix commands?

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: objectives

- Explain what the shell is and why it is essential for microbial genomics workflows.
- Run simple shell commands (`whoami`, `pwd`, `ls`) on a remote server.
- Navigate the directory structure using `cd`, absolute paths, and relative paths.
- Understand how commands, arguments, and options fit together.

::::::::::::::::::::::::::::::::::::::::::::::::::

> This episode is adapted from the Data Carpentry *Introduction to the Command Line for Genomics* lesson and enhanced with concepts needed for microbial genome QC, trimming, assembly, and annotation workflows.

## What is the shell?

The **shell** is a program that interprets your commands and runs other programs.  
Rather than clicking through folders, you **type commands** that give you precise control over:

- navigating files,
- running tools (FastQC, SPAdes, Prokka),
- organizing sequencing data,
- automating workflows.

Because genome-scale tools run on **remote Linux servers**, learning the shell is essential.

When you log in via SSH, you land at a prompt that looks something like:

```bash
learner01@genomics-server:~$
```

Everything typed after this prompt is a command sent to the remote machine.

## Your first commands

Try these:

```bash
whoami
hostname
pwd
```

- `whoami` shows your username (on the **remote server**, not your laptop).
- `hostname` tells you which machine you're logged into.
- `pwd` prints your **present working directory**, letting you confirm where you are.

These help ensure you're operating on the server—not your local machine.

## Listing files with `ls`

Use `ls` to see what’s in your current directory:

```bash
ls
```

Variants:

- `ls -l` – long listing
- `ls -a` – show hidden files (those beginning with `.`)
- `ls -lh` – human-readable file sizes

This is how you inspect data directories like:

```
reads/
trimmed/
assembly/
annotation/
```

as the workshop progresses.

## Moving around with `cd`

You will move between directories constantly during QC, trimming, assembly, and annotation.

```bash
cd directoryname
```

To go **home**:

```bash
cd ~
```

To go **up one level**:

```bash
cd ..
```

To move multiple levels:

```bash
cd ../../
```

To go to a specific path:

```bash
cd /home/learner01/mydata/
```

Understanding paths is critical when feeding files to tools like FastQC or SPAdes.

:::::::::::::::::::::::::::::::::::::::::::::: callout

## Absolute vs relative paths

- **Absolute path:** starts from the root (`/`), e.g.  
  `/home/learner01/mydata/reads/ERR435025_R1.fastq.gz`

- **Relative path:** starts from your current directory, e.g.  
  `reads/ERR435025_R1.fastq.gz`

SPAdes, FastQC, and Prokka all accept either — but incorrect paths are a *very* common error.

::::::::::::::::::::::::::::::::::::::::::::::::::

## Command structure

Commands often look like this:

```
command -option argument
```

Example:

```bash
ls -lh /home/learner01/
```

Later, when you run SPAdes, you'll see the same structure:

```bash
spades.py -1 reads/R1.fastq.gz -2 reads/R2.fastq.gz --threads 10 --memory 120
```

The shell simply interprets the command, options, and arguments you provide.

:::::::::::::::::::::::::::::::::::::::::::::: challenge

## Exercise: Where are you?

Run:

```bash
pwd
```

- What directory are you in?
- Is it your home directory?

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: challenge

## Exercise: Navigate with `cd`

1. Create a directory:
   ```bash
   mkdir practice
   ```
2. Move into it:
   ```bash
   cd practice
   ```
3. Verify location using:
   ```bash
   pwd
   ```

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: challenge

## Exercise: Inspect files with `ls`

In your home directory, run:

```bash
ls -l
ls -a
```

**Questions:**

- Which files are hidden?
- Which items are directories?
- What do the permission strings (like `drwxr-xr-x`) represent?

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: keypoints

- The **shell** is the primary interface for microbial genomics workflows.
- Commands like `whoami`, `hostname`, and `pwd` confirm where you are working.
- `ls` lists files; `cd` moves between directories.
- Understanding paths is essential for running tools like FastQC, SPAdes, and Prokka.
- All commands run on the **remote server**, not your local machine.

::::::::::::::::::::::::::::::::::::::::::::::::::
