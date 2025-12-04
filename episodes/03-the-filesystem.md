---
title: The Filesystem
teaching: 25
exercises: 15
---

:::::::::::::::::::::::::::::::::::::::::::::: questions

- What is the directory (folder) structure on a Linux server, and why should you care?
- How do you create, navigate, and manage directories in the shell?
- What are hidden files, and how can you view them?
- Why does a consistent project directory structure matter for microbial genomics?

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: objectives

- Understand the root filesystem and the concept of a home directory.
- Navigate directories using absolute and relative paths.
- Create, remove, move, and rename files and directories.
- View hidden files and interpret file permissions.
- Apply good directory organization for microbial genomics workflows.

::::::::::::::::::::::::::::::::::::::::::::::::::

## What is the Linux filesystem?

On the server, all files live under the root directory `/`.  
As a learner, you will mainly work in your **home directory**, for example:

```
/home/learner01/
```

This is where all your project files — raw reads, QC results, assemblies, and annotations — should live.

## Why directory structure matters for genomics

A microbial genomics project generates many files (FASTQ, QC outputs, trimmed reads, assembly files, annotation outputs). A clear structure prevents confusion and supports reproducibility.

A recommended layout:

```
myproject/
├── metadata/
├── raw_reads/
├── qc/
├── trimmed/
├── assembly/
├── annotation/
└── scripts/
```

## Navigating directories with `pwd`, `ls`, and `cd`

Check where you are:

```bash
pwd
```

List files:

```bash
ls
ls -l      # long format
ls -a      # include hidden files
ls -lh     # human-readable sizes
```

Move between directories:

```bash
cd directoryname
cd ~        # home
cd ..       # up one level
cd ../../   # up two levels
cd /home/learner01/myproject/
```

:::::::::::::::::::::::::::::::::::::::::::::: callout

## Absolute vs relative paths

**Absolute paths** start from `/`. Example:

```
/home/learner01/myproject/raw_reads/
```

**Relative paths** depend on where you currently are:

```
raw_reads/sample.fastq.gz
```

Understanding paths is essential later when running FastQC, SPAdes, and Prokka.

::::::::::::::::::::::::::::::::::::::::::::::::::

## Creating, moving, copying, and deleting files

```bash
mkdir newdir
cp file1 file2
cp -r dir1 dir2     # copy directories
mv old new
rm file
rm -r directory     # remove directory and contents (dangerous!)
```

:::::::::::::::::::::::::::::::::::::::::::::: callout

### Permissions basics

`ls -l` shows file permissions:

- `r` = read  
- `w` = write  
- `x` = execute  

Directories need `x` permission to be entered.

::::::::::::::::::::::::::::::::::::::::::::::::::

# Exercises

:::::::::::::::::::::::::::::::::::::::::::::: challenge

## Exercise: Explore your home directory

1. Run `pwd` — where are you?  
2. Use `ls -l` — what files or directories do you see?  
3. Use `ls -a` — what hidden files appear?

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: challenge

## Exercise: Create your project skeleton

```bash
mkdir myproject
cd myproject
mkdir metadata raw_reads qc trimmed assembly annotation scripts
```

Run `ls -l`.  
What permissions and sizes do you see?

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: challenge

## Exercise: Copy, move, and delete files

```bash
echo "example" > testfile.txt
cp testfile.txt copy_testfile.txt
mv copy_testfile.txt renamed_testfile.txt
rm testfile.txt
```

Use `ls -l` to confirm results.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: challenge

## Exercise: Clean up & reflect

Return to your home directory:

```bash
cd ~
```

Why is it important that all genomics work stays inside a dedicated project directory?

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: keypoints

- Linux uses a hierarchical filesystem with `/` at the root.
- `pwd`, `ls`, and `cd` are essential tools for navigating the shell.
- Good file organization is critical for genomic workflows.
- Absolute paths are reliable; relative paths depend on your current location.
- Use caution with `rm -r`.

::::::::::::::::::::::::::::::::::::::::::::::::::
