---
title: Why Cloud Computing for Microbial Genomics
teaching: 20
exercises: 10
---

:::::::::::::::::::::::::::::::::::::::::::::: questions

- Why is cloud/HPC computing necessary for microbial genomics?
- What limitations do laptops have for assembly and annotation?
- How does using a remote Unix server improve reproducibility and workflow stability?

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: objectives

- Explain why genomics workflows require more RAM/CPU than personal computers provide.
- Describe the benefits of using a remote server for QC, trimming, assembly, and annotation.
- Recognize how compute resources (CPUs, RAM, storage) impact SPAdes and Prokka.
- Interpret server resource information and understand why it matters for microbial genomics.

::::::::::::::::::::::::::::::::::::::::::::::::::

> This episode integrates core concepts from the Unix tutorial, genome assembly workflow,
> and annotation workflow to explain *why* we rely on powerful remote systems.

## Why local machines aren’t enough

Microbial genomics data are large:

- Illumina paired-end datasets can be large, even exceeding **20 GB**.
- Each FASTQ file may contain **millions of reads**.
- Assembly tools like **SPAdes** can require more than **16 GB of RAM**.
- Annotation tools like **Prokka** load large databases into memory (RAM).

Most laptops cannot handle these resource requirements. Typical problems include:

- Programs freezing due to insufficient memory.
- Disk space running out during assembly.
- Analyses taking many hours or failing entirely.

A remote server solves these issues!

## Practical limitations of remote servers (what to expect)

While cloud and HPC servers provide the resources needed for microbial genomics, they also come with a few practical constraints:

- **Shared resources** – CPU and RAM may be used by many users at once.
- **Storage quotas** – You may run out of disk space and need to clean up or request more.
- **Internet dependence** – If your connection drops, your terminal session may disconnect.
- **Software environments** – Module versions or paths may differ from tutorials online.
- **Login nodes vs compute nodes** – Heavy jobs should not be run on login nodes on some HPC systems.

These constraints are normal in scientific computing.  
One goal of this workshop is learning how to work effectively within them.


:::::::::::::::::::::::::::::::::::::::::::::: callout

## Vocabulary

- **CPU / core** — A processing unit that executes instructions.
- **RAM** — Memory used by running programs; a key limiter for assembly.
- **Disk storage** — Where FASTQ, FASTA, output files, and logs live.
- **Network filesystem** — Shared storage accessible to all users.
- **Remote server** — A powerful, multi-user machine accessed via SSH.

::::::::::::::::::::::::::::::::::::::::::::::::::

## Checking your available resources

Before running heavy tools later (FastQC, trimming, SPAdes, Prokka), it is useful to know how to check:

```bash
df -h .          # check available disk space
free -h          # check memory (RAM)
nproc            # check number of CPU cores
```

These commands help you understand what the server can handle and avoid failed runs due to insufficient resources.

## Why cloud or HPC systems excel at microbial genomics

### 1. More CPUs → Faster assembly  
Later, we'll use the assembly softwsre SPAdes. SPAdes supports threading, which means it can do multiple tasks (or pieces of the task) simultaneously:
```bash
spades.py --threads 10
```
More threads = faster graph construction and contig generation (i.e., faster assembly).

### 2. More RAM → Successful assembly  
If SPAdes runs out of memory, it crashes.  
Servers commonly provide **32–256 GB RAM**, or more.

### 3. High-throughput storage  
Assemblies generate many large temporary files. A server’s storage avoids the “No space left on device” errors common on laptops.

### 4. Reproducibility  
Shared environments load consistent versions:
```bash
fastqc
trimmomatic
spades.py
prokka
```

### 5. Stability  
Jobs can run for **hours** without interruption using `screen` or `tmux`.


## Remote server etiquette & best practices

When working on shared servers:

- Keep file organization tidy (later episodes show how).
- Do not run heavy jobs in your home directory if a `scratch/` or `work/` space is provided.
- Avoid running long jobs in a normal SSH session — use `screen` or `tmux`.
- Delete large temporary files when no longer needed.
- Be mindful that other learners are using the same machine.

Following these practices ensures that everyone can complete the workshop successfully.


## Logging into the remote system

Instructors will provide:

- server hostname  
- username  
- temporary password  

Connect using SSH:
```bash
ssh <username>@<server-address>
```

On macOS/Linux, use:

- Terminal 

On Windows, use:

- Windows Terminal  
- PowerShell  
- PuTTY  
- MobaXterm  

Once connected, you will see a shell prompt:
```bash
learner01@genomics-server:~$
```

## Useful commands for orientation

Here are a few commands you will use repeatedly throughout the workshop:

```bash
whoami      # confirm your user name on the server
hostname    # confirm which machine you are on
pwd         # print your current directory
ls -lh      # list files with readable sizes
```

We will lean heavily on these in every subsequent episode.

:::::::::::::::::::::::::::::::::::::::::::::: challenge

## Exercise: Orient Yourself on the Server

Run the above commands to learn about your current session:

```bash
pwd
```

These confirm you are on the **remote** machine.

::::::::::::::::::::::::::::::::::::::::::::::::::

## How this episode fits into the whole workflow

In later episodes, you will:

1. Use the shell to move, inspect, and organize FASTQ files.  
2. Run FastQC to diagnose read quality.
3. Trim low-quality bases and adapters.
4. Assemble the genome using SPAdes (requires high RAM).
5. Annotate genes using Prokka (requires many CPUs).
6. Interpret assembly and annotation results.

Understanding **why** we use a remote server now will make the computational steps in the rest of the workshop much smoother.

:::::::::::::::::::::::::::::::::::::::::::::: challenge

## Exercise: Why can’t we run SPAdes on a laptop?

Discuss:

1. Why does SPAdes need so much RAM?
2. How large are typical FASTQ input files?
3. What happens if your laptop suspends or sleeps during a long run?
4. How would cloud/HPC resources solve these problems?

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: challenge

## Exercise: Estimate your dataset size

Later in the workshop you will work with FASTQ files. Before assembly, check their sizes:

```bash
du -h reads/
```

**Questions:**

- How large are they?
- Would your laptop have enough free disk space?
- Would you feel confident running SPAdes locally?

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: keypoints

- Sequencing data are large and computationally expensive to assemble.
- Cloud/HPC computing provides the RAM, CPUs, and disk space needed for assembly and annotation.
- You access the remote system through SSH and run all commands *on the server*, not locally.
- Tools like FastQC, Trimmomatic, SPAdes, and Prokka all benefit from shared, stable compute environments.

::::::::::::::::::::::::::::::::::::::::::::::::::
