---
title: Working with Files and Scripts
teaching: 25
exercises: 20
---

:::::::::::::::::::::::::::::::::::::::::::::: questions

- How can I inspect the contents of text files from the command line?
- How do I create, copy, move, and remove files and directories?
- How can I automate a few commands in a simple shell script?

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: objectives

- Use `less`, `head`, and `tail` to view text files.
- Create, copy, move, and remove files and directories with `mkdir`, `cp`,
  `mv`, and `rm`.
- Write and run a small shell script using `bash`.

::::::::::::::::::::::::::::::::::::::::::::::::::

> This episode is adapted from the Data Carpentry *Working with Files and
> Directories* and *Writing Scripts and Working with Data* episodes in
> *Introduction to the Command Line for Genomics*.

## Looking at files: `less`, `head`, and `tail`

Genomics data and results are usually stored in **plain text files**. We can
inspect them from the command line without opening a separate editor.

Navigate to the directory that contains a small text file (for example,
a README or an example FASTQ). Your instructor will give a specific path.

```bash
cd ~/shell_data
ls
```

Use `head` to see the first few lines of a file:

```bash
head README.txt
```

Use `tail` to see the last few lines:

```bash
tail README.txt
```

For longer files, `less` lets you scroll:

```bash
less README.txt
```

- Use the arrow keys or <kbd>Space</kbd> to move.
- Press <kbd>q</kbd> to quit `less`.

## Creating and organizing directories

We often want to separate **raw data**, **intermediate files**, and **results**.

From your home directory, create a project folder structure:

```bash
cd
mkdir microbial_project
cd microbial_project
mkdir data raw qc scripts results
ls
```

Now you have a tidy place to keep files you will create in later episodes.

## Copying, moving, and removing files

The main commands are:

- `cp` – copy files
- `mv` – move or rename files
- `rm` – remove (delete) files
- `mkdir` – create directories
- `rmdir` – remove empty directories

Examples (run from inside `microbial_project`):

```bash
cp ~/shell_data/README.txt data/
ls data

mv data/README.txt data/project_readme.txt
ls data

rm data/project_readme.txt
```

Be careful with `rm` – deleted files are **not** sent to a trash can. They are
gone unless you have a backup.

## A first shell script

Typing the same sequence of commands over and over is error-prone. A **shell
script** is just a text file containing commands that you want to run together.

In the `scripts` directory, create a script called `hello.sh`:

```bash
cd ~/microbial_project/scripts
nano hello.sh
```

In the editor, type:

```bash
#!/usr/bin/env bash

echo "Hello from the microbial genomics workshop!"
pwd
ls
```

- The first line is called a **shebang** and tells the system to run the script
  with `bash`.
- The remaining lines are the same commands you would type at the prompt.

Save the file and exit the editor (your instructor will demonstrate the key
strokes if you are using `nano`).

Run the script:

```bash
bash hello.sh
```

You should see the message, then the working directory, then a listing of the
files in `scripts`.

Optionally, you can mark the script as **executable**:

```bash
chmod +x hello.sh
./hello.sh
```

Now you can run it directly with `./hello.sh`.

:::::::::::::::::::::::::::::::::::::::::::::: challenge

## Exercise: Making a project script

1. From inside `~/microbial_project/scripts`, create a script called
   `setup_project.sh`.
2. The script should:
   - print the current working directory,
   - create directories called `tmp` and `logs` (if they do not already exist),
   - list the contents of the project directory.

3. Run your script from the project root (`~/microbial_project`).

> Hint: use `mkdir -p` to avoid errors if the directory already exists.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: keypoints

## Key Points

- Use `head`, `tail`, and `less` to inspect text files on the command line.
- Use `mkdir`, `cp`, `mv`, and `rm` to manage files and directories.
- A **shell script** is a text file containing commands that can be run
  together with `bash scriptname.sh`.
- Scripts help automate repetitive tasks and make your work more reproducible.

::::::::::::::::::::::::::::::::::::::::::::::::::
