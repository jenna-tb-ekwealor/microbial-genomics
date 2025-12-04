---
title: Project Planning
teaching: 25
exercises: 15
---

:::::::::::::::::::::::::::::::::::::::::::::: questions

- How should I plan a microbial genomics analysis before touching the data?
- What directories, files, and metadata should I set up ahead of time?
- How do I structure a workflow so QC, trimming, assembly, and annotation run smoothly?

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: objectives

- Anticipate the workflow steps in a microbial genomics project.
- Plan a directory layout suitable for QC, trimming, assembly, and annotation workflows.
- Identify metadata you must collect before running tools.
- Understand how planning improves reproducibility and avoids downstream errors.

::::::::::::::::::::::::::::::::::::::::::::::::::

> This episode prepares learners for the workflow used in Episodes 7–11 by building
> the project plan and directory structure needed for quality control, trimming,
> assembly (SPAdes), and annotation (Prokka).  
> It draws on concepts from the Unix tutorial and best practices for genome analysis,
> but does **not** yet introduce FASTQ or tool-specific PDF content.

## Why planning matters

Microbial genomics workflows involve multiple steps:

1. **Quality control** (FastQC)
2. **Trimming**
3. **Genome assembly** (SPAdes)
4. **Assembly evaluation & filtering**
5. **Annotation** (Prokka)
6. **Archiving results & documenting methods**

Each step produces files, logs, and subdirectories. Without planning:

- files become scattered across your home directory,
- output overwrites previous results,
- commands reference the wrong paths,
- reproducibility becomes impossible.

A simple, thoughtful plan prevents all of this.

## Anticipating the workflow

Before analyzing data, ask:

- Where will I store raw FASTQ files?
- Where will QC reports go?
- Where will trimmed reads go?
- Where should the SPAdes assembly output live?
- Where should I store annotation results?
- Where will scripts or notes be kept?

This planning mirrors the Unix skills covered in Episodes 1–5—especially filesystem navigation and working with files.

## Recommended directory skeleton

You can create a clean starting layout:

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

- **metadata/**: sample sheets, run notes  
- **raw_reads/**: original FASTQ files  
- **qc/**: FastQC or other QC outputs  
- **trimmed/**: files after trimming  
- **assembly/**: SPAdes output folders  
- **annotation/**: Prokka output  
- **scripts/**: shell scripts, helper commands  

This structure mirrors the layout used throughout the workshop and is consistent with good practice in microbial genomics research.

:::::::::::::::::::::::::::::::::::::::::::::: callout

### Planning tip

Never mix **raw data** with **processed data**.  
Raw FASTQ files should remain untouched and stored in their own directory.  
All processing steps should write outputs into new directories.

::::::::::::::::::::::::::::::::::::::::::::::::::

## Metadata planning

Before running any tool, you should prepare:

- sample names  
- read file names (R1, R2)  
- sequencing platform  
- expected genome size (helps anticipate memory needs)  
- notes on experimental conditions  

A simple spreadsheet often works best.  
This metadata informs file naming and makes SPAdes/Prokka outputs easier to interpret.

## Planning for tool inputs & outputs

This episode does **not** invoke SPAdes or Prokka directly, but prepares for their behavior:

- SPAdes produces an output directory with many files (logs, contigs, scaffolds, temporary files).
- Prokka outputs multiple files (`.gff`, `.faa`, `.ffn`, `.tbl`, etc.).

Ensuring you already have dedicated directories avoids clutter and accidental overwriting.

:::::::::::::::::::::::::::::::::::::::::::::: challenge

## Exercise: Create your project layout

Make the directory skeleton:

```bash
mkdir -p myproject/{metadata,raw_reads,qc,trimmed,assembly,annotation,scripts}
```

**Questions:**

- Which folder will contain raw FASTQ files?
- Where will SPAdes output go?
- Where should your Prokka annotation end up?

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: challenge

## Exercise: Plan metadata for one sample

Create a text file in the `metadata/` directory:

```bash
echo -e "sample_id\tread1\tread2\nsample01\tsample01_R1.fastq.gz\tsample01_R2.fastq.gz" > metadata/samples.tsv
```

Then inspect it:

```bash
cat metadata/samples.tsv
```

**Question:**  
Why is it helpful to prepare metadata before running analysis tools?

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: keypoints

- Planning your project structure prevents mistakes during multi-step analysis.
- Separate raw data, QC results, trimmed reads, assemblies, and annotations.
- Metadata prepared early improves reproducibility and keeps analyses organized.
- This planning sets the stage for handling FASTQ files starting in Episode 7.

::::::::::::::::::::::::::::::::::::::::::::::::::
