---
title: Trimming and Cleaning Reads
teaching: 30
exercises: 20
---

:::::::::::::::::::::::::::::::::::::::::::::: questions

- Why do we trim and filter raw reads before assembly?
- What kinds of problems can trimming fix?
- How do we run a typical trimming tool on paired-end FASTQ files?
- How do trimmed reads fit into the downstream SPAdes and Prokka workflow?

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: objectives

- Explain why adapter and quality trimming are important for microbial genome assembly.
- Describe common trimming operations (adapter removal, quality trimming, length filtering).
- Run a representative trimming command on paired-end FASTQ files.
- Verify that trimmed reads are created and understand where they should be stored.
- Connect trimming decisions to FastQC results and assembly quality.

::::::::::::::::::::::::::::::::::::::::::::::::::

> This episode builds on the QC step from Episode 8 and the sequencing file formats from Episode 7.
> While your assembly PDF focuses on QC and assembly, trimming is a common intermediate step that
> improves assembly performance and quality, so we discuss it explicitly here.

## Why trim reads?

After QC with FastQC, you may discover:

- low-quality bases at the **3′ ends** of reads,
- **adapter sequences** still present,
- very short or poor-quality reads.

Leaving these issues uncorrected can lead to:

- fragmented assemblies,
- misassemblies,
- wasted compute and storage.

Trimming tools remove or correct problematic parts of reads before assembly.

Common trimming goals:

- remove adapters,
- trim low-quality bases from ends,
- discard reads that become too short.

## Typical trimming workflow

A trimming tool will:

- take **paired-end FASTQ** files as input,
- write new **trimmed** FASTQ files to a different directory,
- optionally produce a log summarizing how many reads were kept or discarded.

A generic command-line pattern looks like:

```bash
trimmer   -i raw_reads/sample01_R1.fastq.gz   -I raw_reads/sample01_R2.fastq.gz   -o trimmed/sample01_R1.trimmed.fastq.gz   -O trimmed/sample01_R2.trimmed.fastq.gz   [options...]
```

The exact options and flags vary by tool (e.g., Trimmomatic, fastp, Cutadapt), but this pattern is common:

- **input reads** → raw FASTQ files,
- **output reads** → trimmed FASTQ files in a separate directory.

:::::::::::::::::::::::::::::::::::::::::::::: callout

### Directory layout reminder

From Episode 6 (Project Planning), trimmed reads should go in a dedicated directory, e.g.:

```
myproject/
├── raw_reads/
├── qc/
├── trimmed/
├── assembly/
└── annotation/
```

Never overwrite your raw FASTQ files when trimming.

::::::::::::::::::::::::::::::::::::::::::::::::::

## Connecting QC to trimming choices

FastQC reports from Episode 8 help answer:

- Are per-base quality scores dropping sharply at the end of reads?
- Do we see clear evidence of adapter contamination?
- Are there overrepresented sequences that look like adapters?

Based on these findings, you might choose to:

- trim the last **10–20 bases** of each read,
- remove known adapter sequences,
- filter out reads below a certain minimum length.

You don’t need to memorize specific thresholds, but you should understand:

- QC → informs trimming  
- Trimming → improves assembly input

## After trimming: checking results

After trimming, you should:

1. Confirm that the new files exist:

```bash
ls trimmed/
```

2. Optionally, run FastQC again on the trimmed reads:

```bash
fastqc -o qc trimmed/sample01_R1.trimmed.fastq.gz trimmed/sample01_R2.trimmed.fastq.gz
```

3. Compare QC reports **before** and **after** trimming:

- Are low-quality tails reduced?
- Are adapter sequences gone or reduced?
- Are length distributions as expected?

The trimmed FASTQ files will be the inputs to **SPAdes** in Episode 10.

---

# Exercises

:::::::::::::::::::::::::::::::::::::::::::::: challenge

## Exercise: Plan your trimming command

Working with a partner and based on your FastQC results:

1. Decide:
   - Do you need adapter trimming?
   - Do you need to cut low-quality bases from the ends?
   - What should your minimum read length be?

2. Draft a pseudocode command (not necessarily using a specific tool yet), e.g.:

```bash
trimmer \
  -i raw_reads/sample01_R1.fastq.gz \
  -I raw_reads/sample01_R2.fastq.gz \
  -o trimmed/sample01_R1.trimmed.fastq.gz \
  -O trimmed/sample01_R2.trimmed.fastq.gz \
  [quality and adapter options...]
```

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: challenge

## Exercise: Check your trimmed files

After running a trimming tool (demonstrated by the instructor):

```bash
ls trimmed/
zcat trimmed/sample01_R1.trimmed.fastq.gz | head -n 4
```

**Questions:**

- Does the file name clearly indicate that the reads are trimmed?
- Can you see that the sequences have been shortened relative to the raw reads?
- How many records remain compared to the original file (`zgrep -c '^@'`)?

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: challenge

## Exercise: QC after trimming

If time permits, run FastQC on the trimmed reads:

```bash
fastqc -o qc trimmed/sample01_R1.trimmed.fastq.gz trimmed/sample01_R2.trimmed.fastq.gz
```

Compare:

- Per-base quality profiles before vs after trimming.
- Overrepresented sequences in both reports.

**Question:**  
Do you think the data are now ready to be used as input to SPAdes?

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: keypoints

- Trimming removes low-quality bases and adapters that can interfere with assembly.
- Trimmed reads should be saved in a separate `trimmed/` directory; raw data must not be overwritten.
- QC (FastQC) guides trimming decisions and can be rerun afterward to confirm improvements.
- Trimmed FASTQ files will be used as inputs to SPAdes in the genome assembly step.

::::::::::::::::::::::::::::::::::::::::::::::::::
