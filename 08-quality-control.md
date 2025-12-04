---
title: Quality Control of Reads
teaching: 30
exercises: 20
---

:::::::::::::::::::::::::::::::::::::::::::::: questions

- Why do we perform quality control (QC) on raw sequencing reads?
- What problems can QC reveal in microbial genomics datasets?
- How do we run FastQC on the command line and interpret its key outputs?
- How does QC inform trimming and assembly decisions?

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: objectives

- Explain why QC is essential before trimming and assembly.
- Run FastQC on compressed FASTQ files.
- Interpret key FastQC metrics (per-base quality, GC content, adapters, sequence duplication).
- Connect QC results to trimming choices and assembly quality.

::::::::::::::::::::::::::::::::::::::::::::::::::

> This episode prepares learners for trimming (Episode 9) and assembly (Episode 10)
> by teaching how to evaluate FASTQ read quality using FastQC.

## Why quality control?

Illumina reads may contain:

- low-quality bases at the 3′ end,
- leftover adapter sequences,
- duplicated reads or biased sequence content,
- poor-quality cycles or lanes.

These issues can:

- reduce assembly contiguity,
- inflate error rates,
- produce misleading downstream analyses.

QC helps you evaluate whether your sequencing run is suitable for assembly and what trimming steps are needed.

## Running FastQC

FastQC accepts `.fastq` and `.fastq.gz` files.

We recommend placing outputs in a dedicated directory:

```bash
mkdir -p qc
fastqc -o qc raw_reads/sample01_R1.fastq.gz raw_reads/sample01_R2.fastq.gz
```

After running:

```bash
ls qc
```

You should see:

- `sample01_R1_fastqc.html`
- `sample01_R1_fastqc.zip`
- `sample01_R2_fastqc.html`
- `sample01_R2_fastqc.zip`

:::::::::::::::::::::::::::::::::::::::::::::: callout

### Viewing FastQC reports

Most learners **download the HTML files** to their local machine and open them in a browser.

Some servers also allow opening them via a remote browser session.

::::::::::::::::::::::::::::::::::::::::::::::::::

## Key FastQC modules

Below are the most important FastQC panels for microbial genomics:

### **Per base sequence quality**
- Boxplots representing quality at each base.
- Declining quality at the 3′ ends usually indicates the need for trimming.

### **Per sequence quality scores**
- Shows the distribution of average read quality.
- Ideally, most reads should fall into high‑quality ranges.

### **Per base sequence content**
- Early cycles often show imbalance; significant deviation across the read is concerning.

### **Per sequence GC content**
- Should approximate a normal distribution.
- A multimodal distribution may indicate contamination or mixed populations.

### **Overrepresented sequences**
- Often indicates adapters, primers, or contamination.
- Will guide which adapter sequences to remove in trimming.

### **Sequence duplication levels**
- Can indicate library prep issues or PCR artifacts.

## Connecting QC → trimming → assembly

QC findings determine trimming strategy (Episode 9):

- Low 3′ quality → trim ends  
- Adapter contamination → remove adapters  
- Short reads after trimming → adjust length filters  

This improves assembly quality in Episode 10.

## Optional: QC on trimmed reads

After trimming:

```bash
fastqc -o qc trimmed/sample01_R1.trimmed.fastq.gz trimmed/sample01_R2.trimmed.fastq.gz
```

Compare trimmed and untrimmed reports to assess improvements.

---

# Exercises

:::::::::::::::::::::::::::::::::::::::::::::: challenge

## Exercise: Run FastQC

Run FastQC on one FASTQ file:

```bash
mkdir -p qc
fastqc -o qc raw_reads/sample01_R1.fastq.gz
```

**Questions:**

- What output files appeared in the `qc/` directory?
- How will you view the HTML report?

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: challenge

## Exercise: Interpret FastQC metrics

With an instructor-provided FastQC report:

- What does the **Per base sequence quality** panel show?
- Are there adapters in the **Overrepresented sequences** panel?
- Would you recommend trimming? Why?

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: challenge

## Exercise: QC after trimming

Compare QC before and after trimming.

**Questions:**

- Did quality scores improve?
- Were adapters removed?
- Are the reads ready for SPAdes assembly?

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: keypoints

- QC is essential before trimming and assembly.
- FastQC summarizes read quality, bias, GC content, and possible contaminants.
- QC results guide trimming decisions.
- Improved trimmed reads lead to better assemblies.

::::::::::::::::::::::::::::::::::::::::::::::::::
