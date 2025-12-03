---
title: Assessing Read Quality (FastQC)
teaching: 20
exercises: 10
---

:::::::::::::::::::::::::::::::::::::::::::::: questions

- How can we quickly assess the quality of our sequencing reads?
- What kinds of problems can we detect with FastQC?
- Where should we store QC reports in our project structure?

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: objectives

- Run FastQC on raw FASTQ files.
- Locate and interpret key plots in a FastQC report.
- Identify common quality issues (low-quality tails, adapter contamination).
- Store QC reports in a dedicated `qc/` directory.

::::::::::::::::::::::::::::::::::::::::::::::::::

> This episode is adapted from the Data Carpentry **Quality Control** episode
> in *Wrangling Genomics*, using FastQC on microbial reads.

## Why do quality control?

Sequencing machines make mistakes. Problems such as:

- declining quality at the ends of reads,
- leftover adapter sequences,
- unexpected sequence content,

can cause trouble for assembly and downstream analyses.

Before trimming or assembly, we run **FastQC** to get an overview of read
quality and potential issues.

## Running FastQC on the rampers server

We will keep all QC outputs in a `qc/` directory inside our project.

From your project root:

```bash
cd ~/microbial_project
mkdir -p qc
fastqc data/raw/*.fastq.gz -o qc
```

This command:

- runs FastQC on all `.fastq.gz` files in `data/raw/`,
- writes HTML and `.zip` reports into `qc/`.

Check the output:

```bash
ls qc
```

You should see files like `sample_R1_fastqc.html` and `sample_R2_fastqc.html`.

## Viewing FastQC reports

FastQC produces HTML files meant to be viewed in a web browser. There are a
few options for seeing them:

- Instructor demo: the instructor downloads one report and shows it on a
  projector.
- Download yourself: use `scp` or an SFTP client to copy `qc/*.html` to your
  local machine and open them in a browser.

The details of downloading will depend on your system; your instructor will
show an example.

## Key FastQC modules

When viewing a FastQC report, pay particular attention to:

- **Per base sequence quality**  
  - Boxplots of quality scores at each base position.  
  - We like to see high-quality scores across most of the read.

- **Per sequence quality scores**  
  - Distribution of mean quality per read.  
  - A unimodal distribution with high scores is good.

- **Per base sequence content**  
  - Proportions of A/C/G/T at each position.  
  - Weird patterns at the start of reads can reflect library prep bias.

- **Adapter content / overrepresented sequences**  
  - Presence of adapter sequences or unexpected motifs.  
  - If adapters are present, trimming is essential.

FastQC uses a red/orange/green flag system (FAIL/WARN/PASS). These are
guidelines, not absolute rules; context matters.

## Deciding what to do next

FastQC does **not** modify your data. It only reports. Based on the report, we
decide:

- whether to trim low-quality bases from read ends,
- whether to remove adapter sequences,
- whether to discard very short or very poor-quality reads.

In the next episode, we will use **fastp** to perform trimming.

:::::::::::::::::::::::::::::::::::::::::::::: challenge

## Exercise: Interpreting a FastQC report

Working from the FastQC report shown by your instructor (or one you download):

1. Is the overall read quality good, fair, or poor?
2. Does quality drop toward the end of the reads?
3. Is there evidence of adapter contamination?
4. Based on the report, what trimming steps seem necessary?

Discuss your answers with a neighbor.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: keypoints

## Key Points

- FastQC provides a quick overview of sequencing read quality.
- We store FastQC reports in a `qc/` directory inside the project.
- Key plots show base quality, sequence quality distribution, and adapter content.
- FastQC helps us decide how aggressively to trim reads before assembly.

::::::::::::::::::::::::::::::::::::::::::::::::::
