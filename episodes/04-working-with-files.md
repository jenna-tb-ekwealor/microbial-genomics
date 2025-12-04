---
title: Working With Files
teaching: 35
exercises: 20
---

:::::::::::::::::::::::::::::::::::::::::::::: questions

- How do I create, view, copy, move, and delete files on the server?
- How do redirection and appending work in the shell?
- Why are file‑handling skills essential for a microbial genomics workflow?

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: objectives

- Create and view files using `touch`, `cat`, `less`, and redirection (`>` and `>>`).
- Copy, move, and rename files using `cp` and `mv`.
- Remove files and directories safely using `rm` and `rmdir`.
- Understand how these operations support QC, trimming, assembly, and annotation workflows.

::::::::::::::::::::::::::::::::::::::::::::::::::

> This episode expands foundational command-line file manipulation skills.
> These skills are essential once you begin handling FASTQ files, QC outputs,
> trimmed reads, SPAdes assemblies, and Prokka annotation results.

## Creating files

Use `touch` to create an empty file:

```bash
touch notes.txt
```

Use `echo` with redirection to write text into a file:

```bash
echo "This is a line of text" > file1.txt    # overwrite
echo "Another line" >> file1.txt             # append
```

:::::::::::::::::::::::::::::::::::::::::::::: callout

## Overwrite vs append

- `>` **overwrites** an existing file  
- `>>` **appends** to the end  

Overwriting raw sequencing data by mistake can ruin an analysis — use redirection carefully.

::::::::::::::::::::::::::::::::::::::::::::::::::

## Viewing files

```bash
cat file1.txt      # print entire file
less file1.txt     # scroll interactively (press q to quit)
head file1.txt     # first 10 lines
tail file1.txt     # last 10 lines
```

These commands are essential later when examining FASTQ structure, assembly summaries, and annotation outputs.

## Copying and moving files

Copy:

```bash
cp file1.txt backup_file1.txt
```

Copy directories:

```bash
cp -r raw_reads/ raw_reads_backup/
```

Move or rename:

```bash
mv file1.txt renamed.txt
mv renamed.txt raw_reads/
```

## Deleting files and directories

Remove a file:

```bash
rm file.txt
```

Remove an empty directory:

```bash
rmdir mydir
```

Remove a directory *and everything inside it*:

```bash
rm -r results/
```

:::::::::::::::::::::::::::::::::::::::::::::: callout
### ⚠️ Warning: `rm -r` is permanent

There is **no undo** in the Unix shell.  
Always double‑check your path before removing a directory.

::::::::::::::::::::::::::::::::::::::::::::::::::

## Why this matters for genomics

Throughout this workshop you will:

- download or receive FASTQ files,  
- inspect QC reports,  
- produce trimmed reads,  
- create SPAdes assembly directories,  
- annotate genomes with Prokka.

Each stage generates multiple files. Clean file-handling habits prevent:

- overwriting raw data,
- losing track of results,
- running tools on the wrong inputs.

Good file management = reproducible science.

# Exercises

:::::::::::::::::::::::::::::::::::::::::::::: challenge

## Exercise: Create and modify a file

1. Create a file:
   ```bash
   touch test.txt
   ```
2. Add a line:
   ```bash
   echo "first line" > test.txt
   ```
3. Append another line:
   ```bash
   echo "second line" >> test.txt
   ```
4. View it with `cat`.

**Questions:**

- What changed between `>` and `>>`?
- Why does this matter for logging workflows?

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: challenge

## Exercise: Copy, move, and rename

```bash
cp test.txt copy_test.txt
mv copy_test.txt renamed_test.txt
mv renamed_test.txt ../   # move one directory up
```

**Questions:**

- Did the file appear where you expected?
- How can you verify using `ls` and `pwd`?

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: challenge

## Exercise: Safe deletions

1. Create a temporary directory:
   ```bash
   mkdir tempdir
   ```
2. Add a file to it:
   ```bash
   echo "data" > tempdir/data.txt
   ```
3. Try to remove with `rmdir tempdir`. What happens?
4. Remove correctly with:
   ```bash
   rm -r tempdir
   ```

**Questions:**  
- Why does `rmdir` only work on empty directories?  
- Why is `rm -r` dangerous?

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: keypoints

- `touch` creates files; `cat` and `less` display them.
- `cp` copies; `mv` renames or moves files/directories.
- `rm` and `rm -r` delete files and directories — permanently.
- Redirection (`>` and `>>`) allows you to create and modify files.
- Good file-handling practices prevent mistakes during genomics workflows.

::::::::::::::::::::::::::::::::::::::::::::::::::
