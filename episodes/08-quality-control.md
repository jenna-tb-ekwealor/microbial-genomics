---
title: Quality Control of Reads
teaching: 30
exercises: 20
---

:::::::::::::::::::::::::::::::::::::::::::::: questions

- Why do we perform quality control (QC) on raw sequencing reads?
- What kinds of issues can QC reveal in microbial genomics datasets?
- How do we run FastQC on the command line and interpret its basic outputs?

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: objectives

- Explain why QC is a critical first step before trimming and assembly.
- Run FastQC on compressed FASTQ files using the command line.
- Locate and view FastQC HTML reports.
- Identify major QC metrics: per-base quality, sequence length, overrepresented sequences, adapters.
- Connect QC findings to downstream decisions (trimming, filtering, assembly).

::::::::::::::::::::::::::::::::::::::::::::::::::

> This episode incorporates the FastQC step described in the *Assembling a Microbial Genome*
> activity and connects it to the sequence file formats from Episode 7. We focus on command‑line
> usage and interpretation of key metrics, even if full QC is abbreviated in class.

## Why quality control?

Raw Illumina reads may contain:

- low‑quality bases at the ends of reads,
- leftover adapter sequences,
- duplicated reads,
- unexpected sequence content.

These issues can:

- decrease assembly quality,
- increase misassemblies,
- waste computational resources.

Quality control with tools like **FastQC** helps you decide:

- whether trimming is necessary,
- which trimming parameters to use,
- whether your data looks as expected.

## FastQC overview

FastQC can be run:

- through a **graphical user interface (GUI)**, or
- on the **command line**.

For a remote server / cloud workflow, the **command‑line approach** is most practical, as described in your assembly activity.

FastQC accepts **FASTQ** (and `.fastq.gz`) files and produces:

- an `.html` report (interactive)
- a `.zip` file containing detailed data

## Running FastQC on the command line

From your assembly exercise, a typical command is:

```bash
fastqc reads/ERR435025_R1.fastq.gz reads/ERR435025_R2.fastq.gz
```

This:

- reads compressed FASTQ files from the `reads/` directory,
- writes HTML and ZIP output files in the current directory.

You can choose an output directory with `-o`:

```bash
mkdir -p qc
fastqc -o qc reads/ERR435025_R1.fastq.gz reads/ERR435025_R2.fastq.gz
```

After running, list the QC directory:

```bash
ls qc
```

You should see files like:

- `ERR435025_R1_fastqc.html`
- `ERR435025_R2_fastqc.html`
- matching `.zip` files

:::::::::::::::::::::::::::::::::::::::::::::: callout

### Viewing FastQC reports

On a remote server, you have two main options:

1. **Download the HTML files** to your local machine (via `scp`, SFTP, or a client like Cyberduck) and open them in a browser.
2. If available, open them directly in a remote browser session (e.g. `firefox` or similar), as suggested in your assembly notes.

In most workshops, downloading and viewing locally is simplest.

::::::::::::::::::::::::::::::::::::::::::::::::::

## Key FastQC modules

Some important panels in the FastQC HTML report include:

- **Per base sequence quality**  
  - Boxplots of quality at each position in the read.  
  - Low quality at the 3′ end often suggests the need for trimming.

- **Per sequence quality scores**  
  - Distribution of average quality per read.

- **Per base sequence content**  
  - Proportions of A/C/G/T at each base position.

- **Per sequence GC content**  
  - Deviations may indicate contamination.

- **Overrepresented sequences**  
  - May reveal adapters or other technical artifacts.

Your goal is not to memorize every module but to recognize:

- whether data quality looks generally **good** or **poor**, and
- whether adapters or other contaminants are present.

## QC in the genome assembly workflow

In the assembly activity, QC is described as an early step, even if it is sometimes skipped in class to save time.

The typical real‑world workflow is:

1. Run **FastQC** on raw FASTQ files.
2. Use the reports to:
   - decide on trimming parameters,
   - confirm read length and quality.
3. Perform **trimming** (next episode).
4. Optionally, run FastQC again on trimmed reads.

Even when abbreviated, understanding the QC step helps interpret downstream assembly quality and potential problems.

---

# Exercises

:::::::::::::::::::::::::::::::::::::::::::::: challenge

## Exercise: Run FastQC on one read file

Assuming your raw reads are in `raw_reads/` or `reads/`, run:

```bash
mkdir -p qc
fastqc -o qc raw_reads/sample01_R1.fastq.gz
```

Then:

```bash
ls qc
```

**Questions:**

- What output files were created?
- How can you transfer the HTML file to your local machine for viewing?

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: challenge

## Exercise: Interpret a FastQC report

Working from an instructor‑provided FastQC HTML report:

- Examine the **Per base sequence quality** module.
- Check whether most bases are in the green (high quality) zone.
- Look at the **Overrepresented sequences** module.

**Questions:**

- Would you recommend trimming this dataset? Why or why not?
- Do you see evidence of adapter contamination?

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: challenge

## Exercise: Connect QC to downstream steps

Discuss with a partner:

1. How could poor QC (low quality, many adapters) affect:
   - genome assembly with SPAdes?
   - annotation with Prokka?

2. How might good QC save time and avoid misleading results?

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: keypoints

- QC is a critical first step before trimming and assembly in microbial genomics.
- FastQC summarizes read quality, sequence content, GC content, and overrepresented sequences.
- FastQC can read compressed `.fastq.gz` files and produces HTML reports for review.
- QC results guide trimming choices and help interpret assembly quality.

::::::::::::::::::::::::::::::::::::::::::::::::::
