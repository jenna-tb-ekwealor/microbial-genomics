---
title: Tidiness & Project Organization
teaching: 25
exercises: 15
---

:::::::::::::::::::::::::::::::::::::::::::::: questions

- Why does tidy organization matter for microbial genomics?
- How should we structure directories for a full analysis workflow?
- How do naming conventions support clarity and reproducibility?

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: objectives

- Organize a microbial genomics project with a clear directory structure.
- Apply consistent file‑naming conventions.
- Understand how tidiness supports transparent, reproducible analysis.
- Prepare a workspace that will be used for QC, trimming, assembly, and annotation.

::::::::::::::::::::::::::::::::::::::::::::::::::

## Why organization matters in genomics

Microbial genomics projects generate many files:  
raw FASTQ, QC reports, trimmed reads, assemblies, annotations, logs, and more.  
Without organization, it becomes easy to:

- run tools on the wrong files,
- overwrite or lose important results,
- confuse raw vs processed data,
- make mistakes that compromise downstream steps.

But beyond convenience, tidy organization is essential for **reproducibility**.

Reproducibility means that:

- *You* can return to your project months later and understand every step.  
- *Another researcher* can recreate your workflow from raw reads to final annotations.  
- Files and directories document the workflow clearly and transparently.

Good structure = good science.

:::::::::::::::::::::::::::::::::::::::::::::: callout

## Naming conventions and reproducibility

Consistent, descriptive naming makes your work understandable.

Good:

```
sample01_R1.fastq.gz
sample01_R2.fastq.gz
trimmed/sample01_R1.trimmed.fastq.gz
assembly/sample01_assembly/
annotation/sample01_prokka/
```

Avoid spaces or ambiguous names:

```
my file.fastq
weirdStuff/
analysis2_final_final/
```

::::::::::::::::::::::::::::::::::::::::::::::::::

## Recommended project directory structure

A clean layout helps separate raw data from processed data:

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

Purpose of each:

- **metadata/**: sample sheets, README files  
- **raw_reads/**: original FASTQ (never modified)  
- **qc/**: FastQC reports and summaries  
- **trimmed/**: files after read trimming  
- **assembly/**: SPAdes results and filtered scaffolds  
- **annotation/**: Prokka outputs  
- **scripts/**: helper scripts, logs, and workflow notes  

This structure mirrors the entire 8‑hour workflow and supports transparent, reproducible analysis.

## Planning for downstream tools

Many tools assume or benefit from a predictable layout:

- FastQC outputs can go in `qc/`
- Trimming outputs go in `trimmed/`
- SPAdes creates an assembly directory inside `assembly/`
- Prokka writes annotation files inside `annotation/`

Clear organization ensures:

- raw data stays untouched,
- intermediate steps remain traceable,
- results are easy to locate and interpret,
- collaborators (or future you) can reproduce the workflow.

:::::::::::::::::::::::::::::::::::::::::::::: callout

## Reproducibility checklist

- [ ] Raw FASTQ lives **only** in `raw_reads/`  
- [ ] QC outputs stored in `qc/`  
- [ ] Trimmed reads stored in `trimmed/`  
- [ ] Assemblies saved in `assembly/`  
- [ ] Annotations saved in `annotation/`  
- [ ] Scripts, notes, and logs saved in `scripts/`  
- [ ] No spaces in filenames  
- [ ] Clear, descriptive naming for all samples  
- [ ] README or metadata file explains the workflow  

::::::::::::::::::::::::::::::::::::::::::::::::::

# Exercises

:::::::::::::::::::::::::::::::::::::::::::::: challenge

## Exercise: Build your project structure

```bash
mkdir -p myproject/{metadata,raw_reads,qc,trimmed,assembly,annotation,scripts}
```

**Questions:**

- Which directories will hold raw vs processed data?
- Why should raw data be kept untouched?

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: challenge

## Exercise: Rename for tidiness

Suppose you received files named:

```
reads1.fq.gz
reads2.fq.gz
```

Rename them:

```bash
mv reads1.fq.gz sample01_R1.fastq.gz
mv reads2.fq.gz sample01_R2.fastq.gz
```

**Why is this important?**

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: challenge

## Exercise: Add documentation

Inside `metadata/`, create a basic README:

```bash
echo "Project: Microbial Genome Workshop
Sample: sample01
Notes: Raw reads stored in raw_reads/, workflow steps recorded in scripts/" > metadata/README.txt
```

Why does this improve reproducibility?

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: keypoints

- Good organization prevents mistakes in multi‑step genomics workflows.
- Clean, consistent naming is essential for clarity and reproducibility.
- A standard directory layout helps trace raw → QC → trimmed → assembly → annotation.
- Documentation (metadata, README, logs) is part of reproducible science.

::::::::::::::::::::::::::::::::::::::::::::::::::
