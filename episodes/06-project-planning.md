---
title: Project Planning
teaching: 25
exercises: 15
---

:::::::::::::::::::::::::::::::::::::::::::::: questions

- How do we plan a microbial genomics workflow before touching the data?
- What directories, metadata, and decisions must be made before QC, trimming, assembly, and annotation?
- How does thoughtful planning support reproducibility and reduce errors?

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: objectives

- Anticipate each stage of the microbial genomics workflow.
- Identify what information (metadata) must be collected before beginning analysis.
- Create a project structure that supports reproducible, traceable computation.
- Understand how planning prevents mistakes and accelerates downstream work.

::::::::::::::::::::::::::::::::::::::::::::::::::

> This episode prepares learners for the complete workflow used in Episodes 7–11:
> sequence formats → QC → trimming → assembly → annotation.
> Good planning prevents downstream confusion and supports transparent, reproducible bioinformatics.

## Why planning matters

Microbial genomics workflows involve many sequential steps:

1. **Quality control** (FastQC)  
2. **Trimming** (removing adapters and low-quality bases)  
3. **Assembly** (SPAdes)  
4. **Contig filtering & evaluation**  
5. **Annotation** (Prokka)  

Each step generates multiple files, and each depends on the previous step being correct.

Good planning ensures that:

- raw data stays untouched,
- workflows are traceable and reproducible,
- directories and filenames are predictable,
- you avoid wasting compute time on mis‑labeled or misplaced files.

Reproducibility begins **before** you run your first command.

## Planning your project structure

You created a tidy project layout in Episode 5.  
Now we expand the rationale behind it.

A clean directory layout enables:

- clear separation of raw vs processed data,
- predictable paths for running tools,
- easy troubleshooting when something fails,
- transparency for collaborators or future you.

A typical workflow structure:

```
myproject/
├── metadata/
├── raw_reads/
├── qc/
├── trimmed/
├── assembly/
├── annotation/
└── scripts/
```

## What metadata do you need?

Before analysis begins, record:

- **sample IDs**  
- **R1 and R2 filenames**  
- **sequencing platform**  
- **expected genome size**  
- **notes about conditions or treatments**  
- **date of sequencing and provider**  

Place metadata in a file inside your project:

```bash
cd myproject/metadata
echo -e "sample_id	read1	read2
sample01	sample01_R1.fastq.gz	sample01_R2.fastq.gz" > samples.tsv
```

Metadata supports:

- reproducibility,
- automation,
- correct input selection,
- downstream interpretation of assembly and annotation.

:::::::::::::::::::::::::::::::::::::::::::::: callout

## Good planning reduces errors

Most failures in QC, trimming, SPAdes, and Prokka come from:
- wrong file paths,
- inconsistent sample names,
- missing metadata,
- unclear project structure.

Planning ahead prevents these issues and saves significant time.

::::::::::::::::::::::::::::::::::::::::::::::::::

## Thinking ahead to QC, trimming, and assembly

Before beginning analysis, confirm:

- Are your raw FASTQ names consistent (`sample01_R1.fastq.gz`, `sample01_R2.fastq.gz`)?  
- Do you know where FastQC outputs will go (`qc/`)?  
- Will trimmed reads be written to (`trimmed/`)?  
- Do you have enough disk space for SPAdes output?  
- Where will Prokka results be saved (`annotation/`)?  

These decisions prevent workflow bottlenecks and unexpected errors mid‑analysis.

## Planning for reproducibility

A reproducible project includes:

- a clear directory tree,
- a metadata file,
- saved scripts or command logs,
- documented decisions (e.g., trimming parameters, SPAdes settings),
- no overwritten raw data,
- version information for tools (FastQC, SPAdes, Prokka).

This ensures others can verify, repeat, or extend your analysis.

# Exercises

:::::::::::::::::::::::::::::::::::::::::::::: challenge

## Exercise: Build a planning checklist

Make a short checklist for your project:

- What directories will you need?
- What metadata must be recorded?
- What filenames will you use?
- Where will QC, trimming, assembly, and annotation outputs go?

Compare with a partner.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: challenge

## Exercise: Create or update your metadata file

```bash
cd myproject/metadata
echo -e "sample_id	read1	read2
sample01	sample01_R1.fastq.gz	sample01_R2.fastq.gz" > samples.tsv
```

**Questions:**

- What additional fields might help future users of this dataset?
- How could you document SPAdes or Prokka parameters here?

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: challenge

## Exercise: Anticipate downstream needs

Discuss:

- What problems might arise if trimmed reads overwrite raw reads?
- Why do we avoid storing large SPAdes outputs inside random directories?
- How does planning help when teaching or collaborating?

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: keypoints

- Good planning prevents errors and supports reproducibility across the workflow.
- Metadata is essential for tracking sample names, files, and decisions.
- A consistent directory structure allows QC → trimming → assembly → annotation to progress smoothly.
- Reproducible science begins before data processing starts.

::::::::::::::::::::::::::::::::::::::::::::::::::
