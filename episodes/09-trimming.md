---
title: Trimming Reads (fastp)
teaching: 15
exercises: 10
---

:::::::::::::::::::::::::::::::::::::::::::::: questions

- Why do we trim sequencing reads before assembly?
- How can we remove low-quality bases and adapter sequences?
- Where do trimmed reads fit in our project directory structure?

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: objectives

- Explain why trimming improves assembly quality.
- Run `fastp` on paired-end reads to produce cleaned FASTQ files.
- Save trimmed reads under `data/trimmed/` and new QC reports under `qc/`.
- Compare the number of reads before and after trimming.

::::::::::::::::::::::::::::::::::::::::::::::::::

> This episode is adapted from the Data Carpentry **Trimming and Filtering**
> episode in *Wrangling Genomics*, using `fastp` instead of Trimmomatic.

## Why trim reads?

FastQC often shows:

- lower quality toward the ends of reads,
- leftover adapter sequence,
- some reads that are too short or poor quality to be useful.

**Trimming** aims to:

- remove low-quality bases from read ends,
- remove adapters,
- discard very short reads after trimming.

The result is a smaller set of **higher-quality reads** that usually assemble
better.

## Project locations for trimmed reads

We will keep trimmed reads in:

```bash
~/microbial_project/data/trimmed
```

and any additional QC reports from fastp in:

```bash
~/microbial_project/qc
```

Create the trimmed directory if needed:

```bash
cd ~/microbial_project
mkdir -p data/trimmed
```

## Running fastp on paired-end reads

Here is a typical `fastp` command for one sample:

```bash
fastp   -i data/raw/sample_R1.fastq.gz   -I data/raw/sample_R2.fastq.gz   -o data/trimmed/sample_R1.trimmed.fastq.gz   -O data/trimmed/sample_R2.trimmed.fastq.gz   -h qc/fastp_sample.html   -j qc/fastp_sample.json
```

This will:

- read `R1` and `R2` files from `data/raw/`,
- write trimmed reads to `data/trimmed/`,
- produce an HTML and JSON report summarizing the trimming.

Your instructor will provide the exact sample filenames used on the rampers
server, or a script that runs `fastp` for multiple samples.

## Inspecting fastp reports

Like FastQC, `fastp` produces an HTML report with:

- basic read statistics,
- quality distributions before and after trimming,
- adapter removal statistics,
- length distributions.

The instructor may demonstrate:

- how many reads were removed,
- how much shorter reads became on average,
- whether adapters were detected and trimmed.

## Checking trimmed files on the server

We can use simple commands to compare raw and trimmed files. For example:

```bash
cd ~/microbial_project

# list raw and trimmed files
ls data/raw
ls data/trimmed

# count lines in one raw vs trimmed file (conceptual)
zcat data/raw/sample_R1.fastq.gz | wc -l
zcat data/trimmed/sample_R1.trimmed.fastq.gz | wc -l
```

Remember to divide the line counts by 4 to get approximate read counts.

:::::::::::::::::::::::::::::::::::::::::::::: challenge

## Exercise: Reasonable trimming or too aggressive?

Using the `fastp` report demonstrated by your instructor (or provided as an
example), answer:

1. What percentage of reads were kept after trimming?
2. Are the per-base quality scores improved after trimming?
3. Did any reads become very short? Would you consider changing the minimum
   length setting?

Discuss with your neighbor how you would adjust trimming parameters if this
were your own project.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: keypoints

- Trimming removes low-quality bases and adapters, improving downstream assembly.
- We keep trimmed reads in `data/trimmed/` and trimming reports in `qc/`.
- `fastp` can handle paired-end trimming and produce summary reports.
- Comparing raw and trimmed statistics helps ensure trimming is reasonable.

::::::::::::::::::::::::::::::::::::::::::::::::::
