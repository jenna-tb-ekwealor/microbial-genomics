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

- Illumina paired-end datasets often exceed **5–20 GB**.
- Each FASTQ file may contain **millions of reads**.
- Assembly tools like **SPAdes** can require **16–120 GB of RAM**.
- Annotation tools like **Prokka** load large databases into memory.

Most laptops cannot handle these resource requirements. Typical problems include:

- Programs freezing due to insufficient memory.
- Disk space running out during assembly.
- Analyses taking many hours or failing entirely.

A remote server solves these issues.

:::::::::::::::::::::::::::::::::::::::::::::: callout

## Vocabulary

- **CPU / core** — A processing unit that executes instructions.
- **RAM** — Memory used by running programs; a key limiter for assembly.
- **Disk storage** — Where FASTQ, FASTA, output files, and logs live.
- **Network filesystem** — Shared storage accessible to all users.
- **Remote server** — A powerful, multi-user machine accessed via SSH.

::::::::::::::::::::::::::::::::::::::::::::::::::

## Why cloud or HPC systems excel at microbial genomics

### 1. More CPUs → Faster assembly  
SPAdes supports threading:
```bash
spades.py --threads 10
```
More threads = faster graph construction and contig generation.

### 2. More RAM → Successful assembly  
If SPAdes runs out of memory, it crashes.  
Servers commonly provide **32–256 GB RAM**, or more.

### 3. High-throughput storage  
Assemblies generate many large temporary files.  
A server’s storage avoids the “No space left on device” errors common on laptops.

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

## Logging into the remote system

Your instructor will provide:

- server hostname  
- username  
- temporary password  

Connect using SSH (macOS/Linux):
```bash
ssh <username>@<server-address>
```

On Windows, use:

- Windows Terminal  
- PowerShell  
- PuTTY  
- MobaXterm  

Once connected, you will see a shell prompt:
```bash
learner01@genomics-server:~$
```

Try:
```bash
whoami
hostname
pwd
```

These confirm you are on the **remote** machine.

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

Later in the workshop you will download real FASTQ files.  
Before assembly, check their sizes:

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
