---
title: Navigating the Filesystem
teaching: 25
exercises: 15
---

:::::::::::::::::::::::::::::::::::::::::::::: questions

- How is data organized on the server?
- How do I move between directories?
- What is the difference between absolute and relative paths?

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: objectives

- Describe the filesystem as a tree of directories and files.
- Use `pwd`, `ls`, and `cd` to move around the filesystem.
- Distinguish between absolute and relative paths.
- Use shortcuts like `.`, `..`, and `~` when specifying paths.

::::::::::::::::::::::::::::::::::::::::::::::::::

> This episode is adapted from the Data Carpentry *Navigating Files and
> Directories* episode in *Introduction to the Command Line for Genomics*.

## The filesystem as a tree

The server stores data in a **filesystem**, which you can picture as a tree:

- the **root** (`/`) at the top,
- directories (folders) as branches,
- files as leaves.

Your personal working area is your **home directory**. On this server, it will
look something like:

```bash
/home/learner01
```

The shell uses **paths** (like addresses) to locate files and directories.

## Where are we? `pwd`

Use `pwd` to **print the working directory**:

```bash
pwd
```

You should see something like `/home/learner01`. This is your starting point.

## What is here? `ls`

Use `ls` to list directory contents:

```bash
ls
```

You should see a directory prepared for the workshop data, for example
`microbial_workshop` or `shell_data`. Your instructor will tell you the exact
name.

You can give `ls` a **path** as an argument:

```bash
ls shell_data
```

This lists the contents of `shell_data` without changing where you are.

## Moving around: `cd`

Use `cd` (*change directory*) to move between directories.

```bash
cd shell_data
pwd
```

Now `pwd` should show that you are inside `shell_data`.

To go **back up one level**, use:

```bash
cd ..
```

To go directly to your home directory from anywhere:

```bash
cd
```

or

```bash
cd ~
```

## Absolute vs relative paths

There are two ways to describe a location:

- **Absolute path** – starts from the root `/` and works downward.
  - Example: `/home/learner01/shell_data/fastq`
- **Relative path** – starts from your current directory.
  - Example: if you are already in `/home/learner01`, then `shell_data/fastq`
    is a relative path to the same place.

Try these commands and compare:

```bash
cd               # go to your home directory
cd shell_data    # relative path
pwd

cd               # back home
cd /home/learner01/shell_data   # absolute path (adjust for your username)
pwd
```

Both commands put you in the same directory.

## Helpful shortcuts

- `.` – the current directory
- `..` – the parent directory
- `~` – your home directory

These shortcuts work in paths. For example:

```bash
cd ~/shell_data
ls ../
```

The second command lists the contents of the directory *above* `shell_data`.

:::::::::::::::::::::::::::::::::::::::::::::: challenge

## Exercise: Navigating the workshop data

Your instructor will tell you the name of the main data directory for this
workshop (for example, `microbial_workshop` or `shell_data`). Starting from
your home directory:

1. Use `cd` and `ls` to find the directory that contains the raw FASTQ files.
2. Use `pwd` to record the **absolute path** to that directory.
3. From the FASTQ directory, use a **relative path** with `cd` to return to
   your home directory.

Compare answers with your neighbor. Did you find the same paths?

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: keypoints

## Key Points

- The filesystem is organized as a **tree** of directories and files.
- `pwd` tells you where you are; `ls` shows what is in a directory; `cd`
  changes your location.
- **Absolute paths** start from `/`; **relative paths** start from your current
  directory.
- Shortcuts like `.`, `..`, and `~` make it easier to specify paths.

::::::::::::::::::::::::::::::::::::::::::::::::::
