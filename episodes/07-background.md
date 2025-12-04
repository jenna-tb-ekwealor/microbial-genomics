---
title: Background: Sequence File Formats
teaching: 30
exercises: 20
---

:::::::::::::::::::::::::::::::::::::::::::::: questions

- What are FASTA, FASTQ, and SAM/BAM file formats?
- How are sequence, identifiers, and quality scores stored?
- Why are many sequence files compressed, and what does `.gz` mean?
- How do these formats fit into the microbial genome assembly and annotation workflow?

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: objectives

- Recognize and describe the structure of FASTA and FASTQ files.
- Understand how quality scores are represented in FASTQ.
- Explain the role of SAM/BAM files in mapping reads to references.
- Identify common filename extensions used in microbial genomics.
- Connect file formats to later workflow steps: QC, trimming, assembly, and annotation.

::::::::::::::::::::::::::::::::::::::::::::::::::

> This episode incorporates concepts from the *Sequence File Formats* notes (FASTA, FASTQ, SAM/BAM)
> and prepares learners to interpret the files used in later episodes for QC, assembly, and annotation.

## Overview of common file types

In microbial genomics, you will frequently encounter:

- **FASTA** – sequence and identifier(s) only  
- **FASTQ** – sequence *and* per-base quality scores  
- **SAM/BAM** – alignments of reads to a reference  

File extensions help you keep track:

- `.fasta`, `.fa`, `.fna`, `.faa`, `.ffn`, `.frn`
- `.fastq`, `.fq`, `.fastq.gz`
- `.sam`, `.bam`

:::::::::::::::::::::::::::::::::::::::::::::: callout

### Plain text vs binary

- FASTA, FASTQ, and SAM are **plain text** (you can read them with `less`).
- BAM is a **binary** version of SAM (smaller and faster to process, not human-readable).

::::::::::::::::::::::::::::::::::::::::::::::::::

## FASTA format

FASTA files store sequence(s) with headers. From your sequence formats notes:

- Header lines start with `>`  
- The header is followed by one or more lines of sequence

Example:

```text
>gi|212499741|ref|YP_002308549.1| DNA polymerase [Bacteriophage APSE-2]
MQNLLFCDLETYSDIPINCGTHRYAENAEILLFAYAYNHAPVKVWDVTQDKTMPADLKAYFDDSEILTVW
HNGGMFDTVILKRVLNIDLPLSRVHDTLVQALAHGLPGALGLLCDIFNVNSDKAKDKEGKALISLLCKPR
```

Key points:

- A FASTA file often contains **many** sequences, one after another.
- FASTA is used for genomes, contigs, proteins, etc.
- Later, SPAdes assemblies and Prokka annotations will use FASTA-formatted files.

## FASTQ format

FASTQ is a **high-density format for short reads** (≤300 nt) that stores both sequence and quality.

Each record has **four lines**:

1. `@` plus an identifier  
2. the raw sequence  
3. `+` (optionally followed by the identifier)  
4. ASCII-encoded quality string  

Example (adapted from your notes):

```text
@DBRHHJN1:387:H89AEADXX:2:1101:1811:1988 1:N:0:TCCTGAGCCTCTCTAT
GTATTGGATATGTCCTCTATTAAACCTTGTGATGAGGAAGCTGTCTGTCTCTTATACACATCTCCGAGCCCACGAGACTCCTGAGCA
+
BB@FFFFFHHHHHJJJJJJJJJJJJJJJJIJJJJJJJJJIJJJIJJJIIIJJJJIJIJJJJJJJJIJHIJJJHHFFDDEEEDDCDDD
```

- Line 1: read name, including run, lane, tile, x/y position, etc.
- Line 2: sequence (A/C/G/T/N).
- Line 4: quality scores encoded as ASCII characters.

These FASTQ files are the **starting point** for QC, trimming, and assembly.

:::::::::::::::::::::::::::::::::::::::::::::: callout

### Why `.fastq.gz`?

FASTQ files are large.  
They are often compressed with **gzip**, resulting in `.fastq.gz` files.

Most tools (FastQC, trimmers, SPAdes) can read gzipped FASTQ directly, so you rarely need to decompress them manually.

::::::::::::::::::::::::::::::::::::::::::::::::::

## SAM and BAM formats

After assembling or mapping reads to a reference, alignments are often stored in **SAM** (text) or **BAM** (binary) format.

A (simplified) SAM snippet from your notes:

```text
@HD VN:1.3 SO:coordinate
@SQ SN:ref LN:45
r001 163 ref 7 30 8M2I4M1D3M = 37 39 TTAGATAAAGGATACTG *
r002 0 ref 9 30 3S6M1P1I4M * 0 0 AAAAGATAAGGATA *
```

Each line after the header contains:

- read name
- flags
- reference name
- position
- CIGAR string (match/mismatch/insertions/deletions)
- sequence and quality

Although this workshop focuses on **de novo assembly** and annotation, you may still encounter SAM/BAM when evaluating assemblies or mapping reads back to contigs.

## Where formats fit into the workflow

- **FASTQ** – raw reads → input to QC and trimming  
- **FASTQ (trimmed)** – input to SPAdes  
- **FASTA** – contigs/scaffolds from assembly → input to annotation (Prokka)  
- **FASTA (proteins, CDS)** – output from Prokka  
- **SAM/BAM** – optional, for read mapping to references or assemblies  

Understanding these formats now will make later steps much less mysterious.

---

# Exercises

:::::::::::::::::::::::::::::::::::::::::::::: challenge

## Exercise: Identify format by eye

Your instructor will show you several short text snippets (or files).  
For each one, decide whether it is:

- FASTA
- FASTQ
- SAM

**Questions:**

- What clues tell you the format?
- How many lines per record can you see?

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: challenge

## Exercise: Inspect a FASTQ file

On the server, navigate to where a small sample FASTQ file is stored and run:

```bash
zcat sample.fastq.gz | head -n 8
```

**Questions:**

- How many complete records are shown in 8 lines?
- Which lines are the sequences?
- Which lines are the quality scores?

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: challenge

## Exercise: Inspect an assembly FASTA file

Later, after running SPAdes, you will have a scaffolds FASTA file.  
Practice on a small example (or instructor-provided file):

```bash
head scaffolds.fasta
```

**Questions:**

- What does each header look like?
- Can you tell how many contigs are in the file (`grep -c '^>' scaffolds.fasta`)?

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: keypoints

- FASTA stores sequence(s) with header lines starting with `>`.
- FASTQ stores reads with **four lines per record**, including quality scores.
- Many FASTQ files are compressed as `.fastq.gz` to save space.
- SAM/BAM store read alignments to a reference genome or assembly.
- Understanding these formats is essential for QC, trimming, assembly, and annotation.

::::::::::::::::::::::::::::::::::::::::::::::::::
