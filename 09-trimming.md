---
title: Trimming Reads
teaching: 30
exercises: 20
---

:::::::::::::::::::::::::::::::::::::::::::::: questions

- Why do we trim raw sequencing reads?
- What kinds of issues can trimming fix?
- How do we run a trimming tool on paired-end FASTQ files?
- How does trimming improve downstream assembly with SPAdes?

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: objectives

- Explain why trimming is an important preprocessing step.
- Describe common trimming tasks (adapter removal, quality trimming, length filtering).
- Run a representative trimming command on paired-end FASTQ files.
- Verify trimmed outputs and understand how they feed into SPAdes assembly.

::::::::::::::::::::::::::::::::::::::::::::::::::

> Raw FASTQ files often contain adapters and low-quality base calls.  
> Trimming cleans the data so assembly (Episode 10) and annotation (Episode 11) perform better.

## Why trim reads?

FastQC (Episode 8) may show:

- low-quality tails at the 3′ end,
- adapter contamination,
- overrepresented sequences,
- poor-quality cycles.

If left untrimmed, these issues can lead to:

- fragmented assemblies,
- misassemblies,
- wasted compute time,
- misleading gene predictions during annotation.

Trimming improves read quality and reduces noise before assembly.

## What does trimming do?

Most trimming tools perform one or more of these steps:

1. **Remove adapters**  
2. **Trim low-quality bases** from the ends  
3. **Filter short reads** below a given length  
4. **Remove unpaired reads** or keep them separately  

In this workshop, trimming is demonstrated with a representative command pattern that applies to tools like `fastp`, `cutadapt`, or `Trimmomatic`.

## Running a trimming tool

A generic trimming command looks like:

```bash
trimmer   -i raw_reads/sample01_R1.fastq.gz   -I raw_reads/sample01_R2.fastq.gz   -o trimmed/sample01_R1.trimmed.fastq.gz   -O trimmed/sample01_R2.trimmed.fastq.gz   [additional options...]
```

Replace `trimmer` with your tool of choice (e.g., `fastp`, `cutadapt`, etc.).

Key arguments:

- `-i` / `-I` → input R1 and R2  
- `-o` / `-O` → output trimmed reads  
- quality, adapter, or length options  

Always write trimmed reads into a **separate directory**, not over raw reads.

:::::::::::::::::::::::::::::::::::::::::::::: callout

## Protect your raw data

Never overwrite your raw FASTQ files.  
Raw reads are considered archival.  
Always place trimmed reads in a new directory:

```
trimmed/sample01_R1.trimmed.fastq.gz
```

::::::::::::::::::::::::::::::::::::::::::::::::::

## Checking trimmed outputs

After trimming:

```bash
ls trimmed/
```

Confirm:

- both `R1` and `R2` trimmed FASTQ files exist,
- their sizes may be smaller than the originals,
- record counts may change depending on trimming parameters.

Optional: run FastQC again to confirm improvements (Episode 8).

## How trimming improves assembly

Cleaner reads → cleaner assembly graph.

Trimming helps:

- reduce ambiguous connections,
- increase contig length,
- reduce memory usage,
- reduce adapter contamination in nodes,
- improve downstream Prokka gene calls.

This prepares your dataset for SPAdes (Episode 10).

---

# Exercises

:::::::::::::::::::::::::::::::::::::::::::::: challenge

## Exercise: Plan your trimming parameters

Based on FastQC:

- Do your reads have low-quality tails?
- Are adapters present?
- What minimum read length makes sense?

Draft a trimming command with options you would use.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: challenge

## Exercise: Run a trimming tool

Your instructor will demonstrate a trimming command.  
Then:

```bash
ls trimmed/
```

**Questions:**

- Did trimmed files appear?
- Are they smaller than raw files?
- How many reads remain versus the original files?

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: challenge

## Exercise: QC after trimming

Run FastQC again (optional):

```bash
fastqc -o qc trimmed/sample01_R1.trimmed.fastq.gz               trimmed/sample01_R2.trimmed.fastq.gz
```

**Questions:**

- Did 3′ quality improve?
- Are adapters still detected?
- Are the reads ready for SPAdes?

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: keypoints

- Trimming removes adapters and low-quality bases that interfere with assembly.
- Always keep raw reads untouched; trimmed reads belong in a separate directory.
- QC results guide trimming choices.
- Good trimming improves SPAdes assembly quality and reduces noise in annotation.

::::::::::::::::::::::::::::::::::::::::::::::::::
