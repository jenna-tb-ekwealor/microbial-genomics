---
site: sandpaper::sandpaper_site
---

Welcome! This workshop covers an 8‑hour introduction to microbial genomics.

Microbial genomics allows us to go from **raw Illumina sequencing reads** to a 
**draft genome** and its **predicted genes**.  
This workshop introduces beginners to the essential skills needed to complete a 
basic microbial genome analysis pipeline using the command line and a remote server.

Over two half-day sessions (8 hours), learners will:

- Connect to and work on a **remote Linux server**
- Use the **Unix shell** to navigate files and run programs
- Perform **FASTQ quality control** and **read trimming**
- Assemble a microbial genome with **SPAdes**
- Annotate genes with **Prokka**
- Understand core biological ideas such as **contigs**, **N50**, **ORFs**, and 
  **start/stop codons**

This workshop is designed for complete beginners and balances short 
conceptual lessons with hands-on practice. We will start with learning the basics of command line languages and software.
Command line interface (CLI) and graphic user interface (GUI) are different ways of interacting with a computer's operating system. They have different pros and cons. Most people are familiar with the GUI as it is the default interface for most software, particularly on Windows and Mac OS. When using the GUI, you see and interact with visual representations of files, folders, applications, and most other functions of your computer.
When using the CLI, you work largely with text representations of software, files, folders, input and output.
The *shell* is a program that allows you to control your computer by typing instructions on the CLI with a keyboard.

There are several reasons to learn how to use the CLI:

- For most bioinformatics tools, there are no graphical interfaces. If you want to work in metagenomics or genomics, you're going to need to use the CLI/ shell.
- The shell gives you power. The command line allows you to work more efficiently. Tasks that are repetitive (e.g. renaming hundreds of files) can be automated. Tasks that are tedious (e.g. testing a range of input parameters) can be simplified.
- To use remote computers or cloud computing, you often need to use the shell.



**PLEASE NOTE:** This is a *pre-alpha* community-developed workshop, **not** a part of The Carpentries' official lesson offerings. However, much of the content is adapted from official Data Carpentry lessons and instructors are actively developing this workshop. 

::::::::::::::::::::::::::::::::::::::::::  prereq

## Getting Started

This lesson assumes **no prior experience** with the command line or genomics.  
Learners should, however, be familiar with basic biological concepts such as DNA, 
genes, and microbial genomes.

Participants should bring their own laptops and be prepared to work on a **remote 
Linux server**.  

To get started, please follow the directions on the 
[Setup page](https://www.jenna-tb-ekwealor.io/genomics-workshop/index.html#setup) to ensure you have access to the required software 
and server environment.

::::::::::::::::::::::::::::::::::::::::::::::::::

---

# Workshop Lessons

| Lesson | Episodes | Overview |
|-------------------------------------|-------------------------------|-------------------------------------|
| **Getting Started: Computing & Shell** | [Computing Concepts & Servers](episodes/01-why-cloud-computing.md)<br>[Introducing the Shell](episodes/02-introduction-to-shell.md)<br>[Navigating the Filesystem](episodes/03-the-filesystem.md)<br>[Working with Files and Scripts](episodes/04-working-with-files.md) | Learn what a server is, why we use remote computing for genomics, and how to use the Unix shell to navigate directories, inspect files, and run basic commands and scripts. |
| **Project Organization for Microbial Genomics** | [Project Tidiness](episodes/05-tidiness.md)<br>[Planning a Genomics Project](episodes/06-project-planning.md) | Organize a microbial genomics project with a clear directory structure, separation of raw vs processed data, and a plan based on organism, genome size, sequencing, and analysis goals. |
| **Sequencing Reads & Quality Control** | [Sequencing Data Background](episodes/07-background.md)<br>[Assessing Read Quality](episodes/08-quality-control.md)<br>[Trimming Reads](episodes/09-trimming.md) | Understand FASTA/FASTQ formats and paired-end reads, then use FastQC and fastp to inspect read quality, remove adapters and low-quality bases, and produce cleaned reads for assembly. |
| **Genome Assembly & Annotation** | [De Novo Assembly with SPAdes](episodes/10-assembly-spades.md)<br>[Genome Annotation with Prokka](episodes/11-annotation-prokka.md) | Assemble trimmed reads into contigs with SPAdes, interpret basic assembly statistics (contig counts, total length, N50), and annotate the resulting genome with Prokka to predict genes and functional features. |

## Optional Additional Lesson

| Lesson | Overview |
| ------------------------------------- | ------------------------------------------------------------------------------------------ |
| [Intro to R and RStudio for Genomics](https://datacarpentry.org/genomics-r-intro/) | Use R to analyze and visualize between-sample variation. |

**Please note that lesson [Intro to R and RStudio for Genomics](https://datacarpentry.org/genomics-r-intro/) is in "beta" development, which means that it is currently being piloted by instructors, but is not yet part of The Carpentries' official lesson offerings.**    

---

# Teaching Platform

This workshop is designed to run on a **remote Linux server** pre-configured with:

- FastQC  
- fastp or Trimmomatic  
- SPAdes  
- Prokka  
- seqkit 

Learners connect via SSH (Terminal, PuTTY, or similar). 

---

# Workshop Schedule (2 half days)

### Half-Day 1

- [Computing concepts & servers](episodes/01-why-cloud-computing.md)  
- [Introducing the shell](episodes/02-introduction-to-shell.md)  
- [Navigating the filesystem](episodes/03-the-filesystem.md)  
- [Working with files and scripts](episodes/04-working-with-files.md)  
- [Project tidiness](episodes/05-tidiness.md) and [Planning a genomics project](episodes/06-project-planning.md)  

### Half-Day 2

- [Sequencing data background](episodes/07-background.md)  
- [Assessing read quality](episodes/08-quality-control.md)  
- [Trimming reads](episodes/09-trimming.md)  
- [Genome assembly with SPAdes](episodes/10-assembly-spades.md)  
- [Genome annotation with Prokka](episodes/11-annotation-prokka.md)  

--- 

::::::::::::::::::::::::::::::::::::::::::  prereq

## For Instructors

If you are teaching this lesson in a workshop, please see the
[Instructor notes](instructors/instructor-notes.md).


::::::::::::::::::::::::::::::::::::::::::::::::::


# Setup

---

## Data Used in This Workshop

This workshop uses a small example dataset of microbial Illumina paired-end reads 
suitable for rapid assembly. These data are provided on the workshop server and do 
not need to be downloaded separately.

