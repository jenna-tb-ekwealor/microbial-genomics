---
title: Tidiness & Project Organization
teaching: 25
exercises: 15
---

:::::::::::::::::::::::::::::::::::::::::::::: questions

- How should we organize files for a microbial genomics project?
- Why is tidy organization essential for QC, trimming, assembly, and annotation workflows?
- What naming conventions and directory structures prevent errors later?

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: objectives

- Explain the importance of tidy project organization in genomics.
- Create a clear directory structure for raw reads, trimmed reads, QC outputs, assemblies, and annotations.
- Apply consistent and meaningful file naming conventions.
- Understand how well‑organized projects reduce mistakes in downstream commands.

::::::::::::::::::::::::::::::::::::::::::::::::::

> This episode uses best practices from the Unix tutorial and prepares for handling
> large datasets and multi-step genomics workflows in later episodes.

## Why organization matters in genomics

Microbial genomics projects quickly accumulate many files:

- raw FASTQ files  
- QC reports  
- trimmed reads  
- assembly outputs  
- annotation files  
- logs and scripts  

Without structure, it becomes easy to:

- run tools on the wrong files,  
- overwrite results,  
- mix up samples, or  
- accidentally delete important data.

A tidy filesystem prevents these mistakes.

## Recommended project structure

A common layout is:

```
project/
├── raw_reads/
├── qc_reports/
├── trimmed/
├── assembly/
├── annotation/
└── scripts/
```

As taught in earlier Unix episodes, this structure uses directories effectively
to keep related files together.

## Naming conventions

Use filenames that are:

- **descriptive**  
- **consistent**  
- **machine‑friendly** (no spaces!)  

Examples:

- `sample01_R1.fastq.gz`
- `sample01_R2.fastq.gz`
- `ERR435025_assembly/`
- `prokka_sample01/`

Avoid:

- `my file.fastq`  
- `data stuff/`  
- `final_FINAL_reallyfinal.txt`

:::::::::::::::::::::::::::::::::::::::::::::: callout

### Tip: Use hyphens or underscores

Good:
```
sample01_R1.fastq.gz
run-2025-reads/
```

Bad:
```
Sample 1 Reads/
```

Spaces break commands unless quoted—dangerous in genomics workflows.

::::::::::::::::::::::::::::::::::::::::::::::::::

## Planning for downstream tools

Later episodes will use:

- **FastQC** → expects clear input filenames  
- **Trimming tools** → produce new FASTQ files  
- **SPAdes** → creates many output directories  
- **Prokka** → generates several annotation files  

A well‑organized structure ensures:

- safe separation of raw vs processed data  
- clarity during command execution  
- easier troubleshooting  
- reproducible workflows

:::::::::::::::::::::::::::::::::::::::::::::: challenge

## Exercise: Build your project structure

Create the recommended structure:

```bash
mkdir -p project/{raw_reads,qc_reports,trimmed,assembly,annotation,scripts}
```

**Questions:**

- Which directories will hold input FASTQ files?
- Where will SPAdes results go?
- Where should you store logs or scripts?

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: challenge

## Exercise: Rename files for tidiness

Suppose you have files:

```
read1.fq.gz
read2.fq.gz
```

Rename them using a good naming convention:

```bash
mv read1.fq.gz sample01_R1.fastq.gz
mv read2.fq.gz sample01_R2.fastq.gz
```

**Question:**  
Why is this better for downstream analysis?

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: keypoints

- Good organization prevents errors in multi-step genomics workflows.
- Use meaningful directory structures: raw reads, QC reports, trimmed data, assemblies, annotations.
- Consistent, space‑free filenames make commands easier and safer.
- Tidy projects support reproducibility and smooth downstream analysis.

::::::::::::::::::::::::::::::::::::::::::::::::::
