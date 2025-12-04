---
title: The Filesystem
teaching: 30
exercises: 20
---

:::::::::::::::::::::::::::::::::::::::::::::: questions

- How is the Unix filesystem organized?
- How do I check where I am in the directory structure?
- How do I move between directories using paths?
- What is the difference between absolute and relative paths?

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: objectives

- Describe how the Unix filesystem is structured.
- Use `pwd` to confirm your current location.
- Navigate into and out of directories using `cd`.
- Distinguish between absolute and relative paths.
- Understand how paths matter for genomic workflows later on.

::::::::::::::::::::::::::::::::::::::::::::::::::

> This episode draws directly from the Unix tutorial PDF (Exercises 2–5) to teach the
> filesystem concepts required before handling FASTQ files, assemblies, or annotations.

## What is the filesystem?

The Unix filesystem is a **tree-like structure** of directories (folders). At the very top is the root:

```
/
```

Below this, you will find directories such as `/home`, `/usr`, `/etc`, etc.

When you log into the workshop server, you start in **your home directory**, represented by:

```
~
```

You can confirm this using:

```bash
pwd
```

This prints your **present working directory** — your current location.

## Listing the contents of a directory

Use `ls` to see what is inside your current directory:

```bash
ls
```

To view more details:

```bash
ls -l
ls -lh
ls -la
```

- `-l` shows long format
- `-h` shows sizes in human-readable units
- `-a` includes hidden files (names beginning with `.`)

## Moving between directories with `cd`

The command `cd` (**change directory**) moves you into a different folder.

Example:

```bash
cd ~
cd mydata
cd ..
```

### Special directories

- `~` — your home directory  
- `.` — the current directory  
- `..` — the parent directory (one level up)

From the Unix tutorial PDF (Exercise 5), you can chain these together:

```bash
cd ~/temp/stuff/things
cd ../../..
```

## Absolute vs relative paths

:::::::::::::::::::::::::::::::::::::::::::::: callout

### Absolute paths
Start with `/` and specify the full path from the root.

Example:

```
/home/learner01/mydata/reads/
```

### Relative paths
Start from your current directory.

Example (from within `mydata`):

```
reads/
```

Understanding this distinction prevents mistakes later when running tools like
FastQC, SPAdes, and Prokka, all of which require accurate file paths.

::::::::::::::::::::::::::::::::::::::::::::::::::

## Combining `pwd`, `cd`, and `ls`

These commands form the navigation toolkit you will use throughout the entire workshop:

```bash
pwd      # where am I?
ls       # what is here?
cd dir   # go somewhere else
cd ..    # go up one level
cd ~     # return home
```

You will use them constantly once you begin working with:

- `reads/` directories,
- `trimmed/` sequence folders,
- SPAdes output directories,
- Prokka annotation folders.

:::::::::::::::::::::::::::::::::::::::::::::: challenge

## Exercise: Explore your home directory

Run:

```bash
pwd
ls -l
```

**Questions:**

1. Which files or directories do you see?
2. Which items are directories?
3. Are any hidden files present?

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: challenge

## Exercise: Practice moving around

1. Create a small directory structure:
   ```bash
   mkdir -p practice/level1/level2
   ```
2. Navigate into the deepest level:
   ```bash
   cd practice/level1/level2
   ```
3. Use `pwd` — what path do you see?
4. Navigate back to your home directory in **one command**.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: challenge

## Exercise: Absolute or relative?

For each path below, decide whether it is absolute or relative:

1. `/home/learner01`
2. `reads/ERR435025_R1.fastq.gz`
3. `../trimmed/`
4. `/usr/bin/`
5. `./scripts/run_spades.sh`

Discuss why absolute paths are often safer when running long workflows.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: keypoints

- The Unix filesystem is a tree with `/` at the root and `~` as your home.
- `pwd` tells you where you are; `ls` shows what is in a directory.
- `cd` moves you between directories using absolute or relative paths.
- Understanding paths is essential for accessing sequencing files and running genomics tools.
- Good navigation skills reduce errors when working with large datasets.

::::::::::::::::::::::::::::::::::::::::::::::::::
