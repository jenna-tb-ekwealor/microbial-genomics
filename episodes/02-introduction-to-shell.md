---
title: Introducing the Shell
teaching: 25
exercises: 15
---

:::::::::::::::::::::::::::::::::::::::::::::: questions

- What is the Unix shell?
- How do I run basic commands on the remote server?
- How do I find help for a command?

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: objectives

- Explain what the shell is and why genomics workflows rely on it.
- Run basic commands such as `whoami`, `pwd`, and `ls`.
- Describe the general structure of a shell command.
- Use tab completion and command history to work more efficiently.
- Use `--help` and `man` to find basic usage information.

::::::::::::::::::::::::::::::::::::::::::::::::::

> This episode is adapted from the Data Carpentry *Introduction to the Command
> Line for Genomics* lesson.

## What is the shell?

The **shell** is a program that takes the commands you type and asks the
operating system to run them. Instead of pointing and clicking in a graphical
interface, you work by typing **text commands**.

For genomics work:

- Many bioinformatics tools are only available on the command line.
- Many tasks involve many files or samples, which are easier to handle with
  scripts.
- Remote servers often only provide a text interface.

## The shell prompt

On our server, your prompt will look something like:

```bash
learner01@genomics-server:~$
```

We will write commands in the lesson like this:

```bash
ls
```

You should **type only what appears after the `$`** and then press
<kbd>Enter</kbd>.

## Your first commands

Try these commands on the server:

```bash
whoami
pwd
ls
```

- `whoami` shows your username.
- `pwd` (*print working directory*) shows where you are in the filesystem.
- `ls` lists files and directories in your current location.

Run `ls` a few times in a row – nothing changes, but this is a good way to
get used to the cycle of **type → Enter → see output**.

## The structure of a command

Most shell commands follow this pattern:

```bash
command  [options]  [arguments]
```

- **command** – the program you are running (e.g. `ls`)
- **options** – extra flags that change behavior (usually start with `-`)
- **arguments** – what the command should act on (files, directories, etc.)

For example:

```bash
ls -lh shell_data
```

- `ls` – list files
- `-lh` – options: `-l` (long format) and `-h` (human-readable sizes)
- `shell_data` – argument: which directory to list

## Getting help

Most commands provide some form of help. Two common patterns:

```bash
ls --help
```

Many programs print a short usage message with `--help` or `-h`.

You can also use manual pages:

```bash
man ls
```

- Use the arrow keys or <kbd>Space</kbd> to scroll.
- Press <kbd>q</kbd> to quit the manual page.

Not every command has a man page, but many core tools do.

## Working more efficiently: history and tab completion

The shell keeps a **history** of commands you have typed.

- Press the **up arrow** to cycle backwards through previous commands.
- Press the **down arrow** to move forward again.

You can also use **tab completion**:

1. Type `ls she` and then press <kbd>Tab</kbd>.
2. If there is only one match (e.g. `shell_data`), the shell completes it.
3. If there are multiple matches, press <kbd>Tab</kbd> twice to see them.

Tab completion works for:

- command names,
- directory names, and
- file names.

:::::::::::::::::::::::::::::::::::::::::::::: challenge

## Exercise: Inspecting the environment

On the remote server, run the following commands:

```bash
whoami
hostname
pwd
ls
ls -lh
```

1. What does each command tell you?
2. What do you think the `-h` option to `ls` does?
3. Try typing `ls -l` and then press the up arrow and edit the command to add
   `h` (so it becomes `ls -lh`).

Discuss your answers with a neighbor.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: challenge

## Exercise: Getting help

1. Use `--help` and/or `man` to answer these questions:

   - Which option to `ls` shows hidden files (those whose names start with `.`)?
   - Which option sorts files by size?

2. Try out your answers on the command line.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: keypoints

- The **shell** lets you control a computer by typing commands instead of using
  a graphical interface.
- A typical command has the form `command [options] [arguments]`.
- `whoami`, `pwd`, and `ls` are useful first commands to confirm where you are
  and what is in a directory.
- Use `--help` or `man` to get basic information about most commands.
- Command history and tab completion save time and reduce typing errors.

::::::::::::::::::::::::::::::::::::::::::::::::::
