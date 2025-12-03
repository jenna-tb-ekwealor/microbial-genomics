---
title: 'Reference'
---

# Glossary


[absolute path]{#absolute-path}
:   A [path](#path) that refers to a particular location in a file
    system. Absolute paths are usually written with respect to the file
    system's

[argument]{#argument}
:   A value given to a function or program when it runs. The term is
    often used interchangeably (and inconsistently) with
    [parameter](#parameter).

[command shell]{#command-shell}
:   See [shell](#shell)

[command-line interface]{#command-line-interface}
:   A user interface based on typing commands, usually at a
    [REPL](#read-evaluate-print-loop). See also: [graphical user
    interface](#graphical-user-interface).

[comment]{#comment}
:   A remark in a program that is intended to help human readers
    understand what is going on, but is ignored by the computer.
    Comments in Python, R, and the Unix shell start with a `#` character
    and run to the end of the line; comments in SQL start with `--`, and
    other languages have other conventions.

[current working directory]{#current-working-directory}
:   The directory that [relative paths](#relative-path) are calculated
    from; equivalently, the place where files referenced by name only
    are searched for. Every [process](#process) has a current working
    directory. The current working directory is usually referred to
    using the shorthand notation `.` (pronounced "dot").

[file system]{#file-system}
:   A set of files, directories, and I/O devices (such as keyboards and
    screens). A file system may be spread across many physical devices,
    or many file systems may be stored on a single physical device; the
    [operating system](#operating-system) manages access.

[filename extension]{#filename-extension}
:   The portion of a file's name that comes after the final "."
    character. By convention this identifies the file's type: `.txt`
    means "text file", `.png` means "Portable Network Graphics file",
    and so on.

[filter]{#filter}
:   A program that transforms a stream of data.

[flag]{#flag}
:   A terse way to specify an option or setting to a command-line
    program.

[for loop]{#for-loop}
:   A loop that is executed once for each value in some kind of set,
    list, or range.

[graphical user interface]{#graphical-user-interface}
:   A user interface based on selecting items and actions from a
    graphical display.

[home directory]{#home-directory}
:   The default directory associated with an account on a computer
    system.

[loop]{#loop}
:   A set of instructions to be executed multiple times.

[loop body]{#loop-body}
:   The set of statements that are repeated inside loops.

[MIME type]{#mime-type}
:   File type conventions used on the Internet.

[operating system]{#operating-system}
:   Software that manages interactions between users, hardware, and
    processes.

[parameter]{#parameter}
:   A variable named in a function's declaration.

[parent directory]{#parent-directory}
:   The directory that contains the current one.

[path]{#path}
:   A description specifying a file or directory location.

[pipe]{#pipe}
:   A connection from one program's output to another's input.

[process]{#process}
:   A running instance of a program.

[prompt]{#prompt}
:   Characters displayed by a REPL awaiting input.

[quoting]{#quoting}
:   Using quotation marks to prevent shell interpretation.

[read-evaluate-print loop]{#read-evaluate-print-loop}
:   A command loop that reads, executes, prints, repeats.

[redirect]{#redirect}
:   Sending command output to a file or reading input from a file.

[regular expression]{#regular-expression}
:   A pattern describing allowed character sequences.

[relative path]{#relative-path}
:   A path interpreted relative to the current working directory.

[root directory]{#root-directory}
:   The top-most directory in a filesystem.

[shell]{#shell}
:   A command-line interface (e.g. Bash).

[shell script]{#shell-script}
:   A set of shell commands stored in a file.

[standard input]{#standard-input}
:   A process's default input stream.

[standard output]{#standard-output}
:   A process's default output stream.

[sub-directory]{#sub-directory}
:   A directory contained within another.

[tab completion]{#tab-completion}
:   Automatic completion triggered by pressing Tab.

[variable]{#variable}
:   A name associated with a value in a program.

[while loop]{#while-loop}
:   A loop that executes while a condition is true.

[wildcard]{#wildcard}
:   A character used in pattern matching.


---


# Command-Line Cheat Sheet

This page summarizes the main shell commands used in:

- 07: Sequencing Data Background  
- 08: Assessing Read Quality (FastQC)  
- 09: Trimming Reads (fastp)  
- 10: De Novo Assembly with SPAdes  
- 11: Genome Annotation with Prokka  

## General navigation

```bash
cd ~/microbial_project          # go to project root
ls                              # list files in current directory
ls data/raw                     # list raw FASTQ files
ls data/trimmed                 # list trimmed FASTQ files
ls qc                           # list QC reports
ls assembly                     # list assembly outputs
ls annotation                   # list annotation outputs
```

## Sequencing data locations (Episode 07)

```bash
cd ~/microbial_project
ls data/raw                     # check raw FASTQ files
```

(Conceptual) Counting lines/reads in a FASTQ file:

```bash
zcat data/raw/sample_R1.fastq.gz | wc -l   # number of lines
# number of reads = (lines / 4)
```

## Running FastQC (Episode 08)

```bash
cd ~/microbial_project
mkdir -p qc
fastqc data/raw/*.fastq.gz -o qc
ls qc
```

FastQC reports are HTML files such as:

- `sample_R1_fastqc.html`
- `sample_R2_fastqc.html`

You can download these to your local machine and view them in a browser.

## Running fastp for trimming (Episode 09)

```bash
cd ~/microbial_project
mkdir -p data/trimmed

fastp   -i data/raw/sample_R1.fastq.gz   -I data/raw/sample_R2.fastq.gz   -o data/trimmed/sample_R1.trimmed.fastq.gz   -O data/trimmed/sample_R2.trimmed.fastq.gz   -h qc/fastp_sample.html   -j qc/fastp_sample.json
```

Comparing raw vs trimmed (conceptual):

```bash
ls data/raw
ls data/trimmed

zcat data/raw/sample_R1.fastq.gz | wc -l
zcat data/trimmed/sample_R1.trimmed.fastq.gz | wc -l
```

## Running SPAdes (Episode 10)

```bash
cd ~/microbial_project
mkdir -p assembly

spades.py   -1 data/trimmed/sample_R1.trimmed.fastq.gz   -2 data/trimmed/sample_R2.trimmed.fastq.gz   -o assembly/spades_sample
```

Inspecting assembly output:

```bash
ls assembly/spades_sample                          # list SPAdes outputs
grep -c "^>" assembly/spades_sample/contigs.fasta  # count contigs
head -n 20 assembly/spades_sample/contigs.fasta    # preview first contig
```

If `seqkit` is available:

```bash
seqkit stats assembly/spades_sample/contigs.fasta
```

## Running Prokka (Episode 11)

```bash
cd ~/microbial_project
mkdir -p annotation

prokka   --outdir annotation/sample   --prefix sample   assembly/spades_sample/contigs.fasta
```

Inspecting Prokka outputs:

```bash
ls annotation/sample

grep -c "\tCDS\t" annotation/sample/sample.gff   # count CDS features
less annotation/sample/sample.txt                  # summary of annotation
head annotation/sample/sample.faa                  # preview protein sequences
```

## Tips

- Use `Tab` to auto-complete filenames and directories.
- Use the up arrow to repeat and edit previous commands.
- Keep commands that worked well in a text file or shell script for reuse.

---

# External references

### Opening a terminal

- [How to Use Terminal on a Mac](https://www.macworld.co.uk/feature/mac-software/how-use-terminal-on-mac-3608274/)
- [Git for Windows](https://git-for-windows.github.io/)
- [How to Install Bash shell command-line tool on Windows 10](https://www.windowscentral.com/how-install-bash-shell-command-line-windows-10)
- [Install and Use the Linux Bash Shell on Windows 10](https://www.howtogeek.com/249966/how-to-install-and-use-the-linux-bash-shell-on-windows-10/)
- [Using the Windows 10 Bash Shell](https://www.howtogeek.com/265900/everything-you-can-do-with-windows-10s-new-bash-shell/)
- [Using a UNIX/Linux emulator (Cygwin) or Secure Shell (SSH) client (Putty)](https://faculty.smu.edu/reynolds/unixtut/windows.html)
- [Addressing the digital divide in contemporary biology: Lessons from teaching UNIX](https://www.biorxiv.org/content/early/2017/04/07/122424.full.pdf+html)
- [Unix cheat sheet](https://files.fosswire.com/2007/08/fwunixref.pdf)

### Manuals

- [GNU BASH reference](https://www.gnu.org/software/bash/manual/html_node/index.html)
- [GNU manual](https://www.gnu.org/manual/manual.html)
- [Core GNU utilities](https://www.gnu.org/software/coreutils/manual/coreutils.html)

### FASTQ files

- [Phred quality score](https://en.wikipedia.org/wiki/Phred_quality_score)
- [FASTQ format](https://en.wikipedia.org/wiki/FASTQ_format)

### High-throughput sequencing

- Illumina Sequencing Technology [YouTube video](https://www.youtube.com/watch?v=womKfikWlxM)

