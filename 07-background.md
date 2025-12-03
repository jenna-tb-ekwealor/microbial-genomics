---
title: Sequencing Data Background
teaching: 15
exercises: 5
---

:::::::::::::::::::::::::::::::::::::::::::::: questions

- What is the difference between FASTA and FASTQ files?
- What information is stored in a sequencing read?
- What are paired-end reads, and why do we use them?
- Where will our sequencing files live on the rampers server?

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: objectives

- Distinguish between FASTA and FASTQ formats.
- Describe the four lines that make up a single FASTQ record.
- Explain what paired-end reads are and how they are named.
- Locate the raw FASTQ files for this workshop in your project directory.

::::::::::::::::::::::::::::::::::::::::::::::::::

> This episode is adapted from the Data Carpentry **Wrangling Genomics** 
> background lesson and a short sequence file formats overview, condensed for
> microbial assembly.

## Sequences, reads, and genomes

- A **genome** is the complete DNA sequence of an organism.
- A **read** is a short piece of DNA sequence produced by a sequencer.
- To reconstruct a genome, we need many overlapping reads.

In this workshop, we work with **Illumina paired-end reads** from a single
microbial genome. The goal is to assemble these reads into **contigs** and then
annotate genes.

## FASTA vs FASTQ

Both FASTA and FASTQ are text formats used to store sequences.

- **FASTA** stores only the **sequence**.
- **FASTQ** stores the **sequence plus a quality score** for each base.

A FASTA record looks like:

```text
>sequence_id
ACGTACGTACGT...
```

A FASTQ record always has **four lines per read**:

1. `@` + sequence identifier  
2. DNA sequence  
3. `+` (optionally followed by the identifier again)  
4. Quality string (one character per base)

For example:

```text
@read0001
ACGTACGTACGT
+
IIIIHHHFFFEE
```

The quality string encodes how confident the sequencer is about each base
(higher characters = better quality). We will not decode the exact scores in
this workshop, but we will look at **quality profiles** with FastQC.

## Compressed FASTQ files

On the rampers server, sequencing reads are usually stored in compressed
files with the `.fastq.gz` extension. These are FASTQ files that have been
compressed with `gzip` to save disk space.

Example filenames:

- `sample_R1.fastq.gz` – forward reads  
- `sample_R2.fastq.gz` – reverse reads  

The `R1` and `R2` indicate the two **ends** of the same DNA fragment.

## Paired-end reads

In **paired-end sequencing**, the machine reads from both ends of each DNA
fragment, producing two reads per fragment:

- `R1` – read from one end
- `R2` – read from the other end

These pairs:

- improve mapping and assembly,
- help resolve small repeats,
- give more confidence about insert size.

Assemblers like SPAdes expect these reads to be provided as matching `R1` and
`R2` FASTQ files.

## Where are our reads on the rampers server?

For this workshop we will keep raw data in:

```bash
~/microbial_project/data/raw
```

Check that directory now:

```bash
cd ~/microbial_project
ls data/raw
```

You should see one or more pairs of FASTQ files (e.g. `sample_R1.fastq.gz` and
`sample_R2.fastq.gz`). Your instructor will describe the specific dataset.

:::::::::::::::::::::::::::::::::::::::::::::: challenge

## Exercise: Counting reads (conceptual)

The total number of reads in a FASTQ file is the number of lines divided by 4.

Without actually running the commands, answer:

1. Which command would show you the number of lines in a compressed FASTQ?
2. How would you compute the approximate number of reads from that?

Your instructor may demonstrate this on the rampers server.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: keypoints

- FASTA stores **sequence only**; FASTQ stores **sequence plus quality**.
- Each FASTQ read uses four lines: identifier, sequence, separator, qualities.
- Illumina paired-end data is stored as `R1` and `R2` FASTQ files.
- We keep raw reads in `~/microbial_project/data/raw` on the rampers server.

::::::::::::::::::::::::::::::::::::::::::::::::::
