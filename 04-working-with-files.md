---
title: Working With Files
teaching: 35
exercises: 20
---

:::::::::::::::::::::::::::::::::::::::::::::: questions

- How do I create, view, copy, move, and delete files in Unix?
- How do I redirect output to files?
- How do these skills prepare us for handling FASTQ, FASTA, QC, trimming, and assembly outputs?

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: objectives

- Create empty files using `touch`.
- View file contents using `cat`, `less`, and redirection.
- Copy and move files using `cp` and `mv`.
- Delete files and directories safely using `rm` and `rmdir`.
- Use redirection (`>`, `>>`) to create and modify files.
- Build comfort with file manipulation before working with large genomics datasets.

::::::::::::::::::::::::::::::::::::::::::::::::::

> This episode incorporates content from the Unix tutorial PDF (Exercises 7–11),
> focusing on file creation, editing, copying, moving, and deletion. These skills
> directly support genomics workflows where FASTQ, trimmed reads, assemblies,
> and annotation outputs must be manipulated.

## Creating new files with `touch`

From the Unix tutorial (Exercise 7), `touch` creates an empty file:

```bash
touch notes.txt
```

Check that it exists:

```bash
ls -l
```

You will later use this skill when organizing metadata, scripts, logs, and assembly outputs.

## Redirecting output with `>` and `>>`

The `echo` command prints text.  
Pair it with redirection to send output into files (Unix tutorial Exercise 8).

### Overwrite a file:

```bash
echo "Quality control complete." > log.txt
```

### Append to a file:

```bash
echo "Assembly started at: $(date)" >> log.txt
```

:::::::::::::::::::::::::::::::::::::::::::::: callout

### Overwrite vs append

- `>` replaces the entire file (use cautiously).
- `>>` adds new text at the end (safe for logging).

These are especially important when capturing quality control and assembly logs later.

::::::::::::::::::::::::::::::::::::::::::::::::::

## Viewing files with `cat` and `less`

- `cat filename` prints the whole file at once.
- `less filename` allows scrolling (`q` to quit).

These tools are essential for inspecting:

- FASTQ headers
- log files
- assembly reports
- annotation summaries

Example:

```bash
less log.txt
```

## Copying files with `cp`

From the Unix tutorial (Exercise 9):

```bash
cp original.txt backup.txt
```

Copy to a directory:

```bash
cp notes.txt archive/
```

Copy entire directories:

```bash
cp -r results/ results_backup/
```

This becomes essential when backing up read files before quality trimming or assembly.

## Moving or renaming files with `mv`

`mv` can move **or** rename files:

```bash
mv draft.txt final.txt
mv final.txt documents/
```

You will later use this to organize outputs such as:

- `ERR435025_assembly/`
- trimmed reads directories
- annotation output folders

## Removing files and directories

### Remove a file:

```bash
rm oldfile.txt
```

### Remove an empty directory:

```bash
rmdir emptydir
```

### Remove a directory *with contents*:

```bash
rm -rf tempdir
```

:::::::::::::::::::::::::::::::::::::::::::::: callout

### Warning: `rm -rf`

This command deletes **everything** in a directory **permanently** and **cannot be undone**.

Use it carefully, especially when working with important read files or assemblies.

::::::::::::::::::::::::::::::::::::::::::::::::::

## Editing files with `nano`

Open a file for editing:

```bash
nano notes.txt
```

Use:

- `Ctrl + O` to save
- `Ctrl + X` to exit

Log files, small scripts, and metadata files can all be edited this way.

---

# Exercises

:::::::::::::::::::::::::::::::::::::::::::::: challenge

## Exercise: Create and inspect files

1. Create a file:
   ```bash
   touch example.txt
   ```
2. Add text using `>`:
   ```bash
   echo "First line" > example.txt
   ```
3. Append text:
   ```bash
   echo "Second line" >> example.txt
   ```
4. View using:
   ```bash
   cat example.txt
   ```

**Questions:**  
- What happened when you used `>`?  
- What changed when you used `>>`?

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: challenge

## Exercise: Copy and move files

1. Copy your file:
   ```bash
   cp example.txt example_copy.txt
   ```
2. Make a directory:
   ```bash
   mkdir workspace
   ```
3. Move both files into the directory:
   ```bash
   mv example*.txt workspace/
   ```

**Question:**  
- How can you confirm that the files moved successfully?

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: challenge

## Exercise: Remove files safely

1. Make a directory with files:
   ```bash
   mkdir testdir
   echo "data" > testdir/a.txt
   ```
2. Try:
   ```bash
   rmdir testdir
   ```
   Why does it fail?
3. Remove the directory properly:
   ```bash
   rm -r testdir
   ```

Discuss safety concerns around using `rm -rf`.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: keypoints

- `touch` creates files; `cat` and `less` view them.
- `cp` copies files; `mv` moves or renames them.
- `rm` and `rmdir` delete files or directories.
- `>` overwrites files; `>>` appends to them.
- These skills are essential for managing reads, QC logs, assemblies, and annotation outputs.
- Be extremely careful when removing directories, especially with `rm -rf`.

::::::::::::::::::::::::::::::::::::::::::::::::::
