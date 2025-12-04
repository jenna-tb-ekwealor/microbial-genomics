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
- Use `pwd`, `ls`, and `cd` to navigate the directory structure.
- Distinguish between absolute and relative paths.
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

Everything typed after this prompt is interpreted *by the remote machine*.

## Confirming your location

You can check where you are using:

```bash
pwd
```

This prints the **present working directory**, which will usually be your home directory when you first log in.

## Listing files with `ls`

Use `ls` to see what’s in your current directory:

```bash
ls
```

Common useful variations:

- `ls -l` – long listing with details  
- `ls -a` – show hidden files (those beginning with `.`)  
- `ls -lh` – human-readable sizes  

## Moving around with `cd`

You will move between directories throughout the workshop:

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
cd /home/learner01/myproject/
```

:::::::::::::::::::::::::::::::::::::::::::::: callout

## Absolute vs relative paths

- **Absolute path:** starts from the root (`/`), e.g.  
  `/home/learner01/myproject/raw_reads/`

- **Relative path:** starts from your *current* directory, e.g.  
  `raw_reads/ERR435025_R1.fastq.gz`

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

:::::::::::::::::::::::::::::::::::::::::::::: callout  
### Common beginner mistakes

| Mistake | What to check / avoid |
|--------|----------------------|
| Running commands in the wrong directory | Always run `pwd` to confirm location |
| Using relative paths carelessly | Prefer absolute paths for important commands |
| Overwriting or deleting files by accident | Double-check filenames; avoid spaces in names |
| Confusing local vs remote context | After SSH login, all commands run on the **remote server** |

::::::::::::::::::::::::::::::::::::::::::::::::  

# Exercises

:::::::::::::::::::::::::::::::::::::::::::::: challenge

## Exercise: Where are you?

Run:

```bash
pwd
```

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: challenge

## Exercise: Navigate with `cd`

```bash
mkdir practice
cd practice
pwd
```

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: challenge

## Exercise: Inspect files with `ls`

```bash
ls -l
ls -a
```

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: challenge

## Exercise: Practice navigation and paths  

1. Use `pwd` to confirm your current directory.  
2. Create a directory named `practice1`.  
3. Change into it.  
4. Create and move into a subdirectory:
```bash
mkdir subdir
cd subdir
```
5. Navigate back to your home directory in one command.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: keypoints

- The **shell** is the primary interface for microbial genomics workflows.
- `pwd`, `ls`, and `cd` are essential tools for navigation.
- Understanding paths is critical for running tools like FastQC, SPAdes, and Prokka.
- All commands run on the **remote server**, not your local machine.

:::::::::::::::::::::::::::::::::::::::::::::::::
