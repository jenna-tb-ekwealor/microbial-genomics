---
title: Genome Annotation with Prokka
teaching: 40
exercises: 20
---

:::::::::::::::::::::::::::::::::::::::::::::: questions

- What is genome annotation, and why do we perform it after assembly?
- How do we run Prokka on an assembled microbial genome?
- What Prokka options are most important for typical bacterial genomes?
- What kinds of output files does Prokka produce, and how can we use them?

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: objectives

- Explain the purpose of genome annotation in microbial genomics.
- Run Prokka on an assembled genome using sensible options.
- Interpret the most important annotation output files (GFF, FAA, FFN, GBK, etc.).
- Understand the difference between annotating a single genome, a bin, or a metagenome.
- Connect annotation results to downstream analyses (comparative genomics, visualization, etc.).

::::::::::::::::::::::::::::::::::::::::::::::::::

> This episode is based on your Prokka annotation exercise and follows directly from
> the SPAdes assembly in Episode 10. We assume that a scaffold FASTA file is available
> and that contigs have already been filtered to a reasonable minimum length.

## What is genome annotation?

Genome annotation is the process of:

- finding genes (CDS) and other features (tRNAs, rRNAs),
- predicting their functions,
- assigning standardized names and identifiers.

For a microbial genome, annotation helps you answer:

- How many protein-coding genes are present?
- Are there plasmids, phage, or mobile elements?
- Which pathways or functions are encoded?

**Prokka** is a widely used tool for **rapid, automated annotation** of bacterial and archaeal genomes.

## Inputs and outputs of Prokka

Prokka expects:

- a FASTA file of contigs (e.g. scaffolds from SPAdes),
- basic options describing the run and the organism.

It produces:

- `.gff` – combined sequence and annotation
- `.gbk` – GenBank-format file
- `.faa` – protein sequences
- `.ffn` – nucleotide sequences of genes
- `.fna` – nucleotide sequences of contigs
- `.tbl` – feature table
- `.txt` – plain-text summary
- other helper files

These outputs can be loaded into genome browsers, comparative genomics tools, or downstream pipelines.

## Basic Prokka command

From your Prokka exercise, the generic form is:

```bash
prokka [options] mysequences.fna
```

For a typical genome or metagenome bin, your notes suggest:

```bash
prokka \
  --outdir OUTPUTDIRECTORY \
  --prefix OUTPUTFILE_PREFIX \
  --addgenes \
  --locustag MYGEN \
  --increment 5 \
  --cpus 20 \
  --mincontiglen 1000 \
  MYSEQUENCEFILE
```

We will adapt this to our workshop data.

## Running Prokka on a SPAdes assembly

Assume you have a scaffold FASTA file from Episode 10, such as:

- `scaffolds.fasta`
- or a filtered version with contigs ≥ 1000 bp.

From your `annotation/` directory:

```bash
cd myproject/annotation
cp ../assembly/scaffolds.fasta sample01.scaffolds.fasta
```

Run Prokka:

```bash
prokka \
  --outdir sample01_prokka \
  --prefix sample01 \
  --addgenes \
  --locustag S01 \
  --increment 5 \
  --cpus 8 \
  --mincontiglen 1000 \
  sample01.scaffolds.fasta
```

Adjust:

- `--cpus` for your system,
- `--locustag` and `--prefix` for your organism or project,
- `--mincontiglen` if you want a different minimum contig size.

:::::::::::::::::::::::::::::::::::::::::::::: callout

### Prokka for metagenomes

Your notes distinguish:

- **Genome or bin** annotation:
  ```bash
  prokka --outdir OUT --prefix PREFIX --addgenes --locustag TAG --increment 5 --cpus 20 --mincontiglen 1000 MYSEQUENCEFILE
  ```
- **Entire metagenome** annotation:
  ```bash
  prokka --outdir OUT --prefix PREFIX --addgenes --metagenome --locustag TAG --increment 5 --cpus 20 --mincontiglen 1000 MYSEQUENCEFILE
  ```

The `--metagenome` flag adjusts gene prediction for fragmented genomes.

::::::::::::::::::::::::::::::::::::::::::::::::::

## Inspecting Prokka output

After Prokka finishes, list the output directory:

```bash
ls sample01_prokka
```

Look for:

- `sample01.gff`
- `sample01.gbk`
- `sample01.faa`
- `sample01.ffn`
- `sample01.fna`
- `sample01.tbl`
- `sample01.txt`

You can inspect the summary file:

```bash
less sample01.txt
```

It typically includes:

- number of CDS,
- number of tRNAs and rRNAs,
- contig statistics,
- basic annotation summary.

View the GFF header:

```bash
head sample01.gff
```

This file is especially useful because it:

- combines sequence,
- feature coordinates,
- annotations,

in a single standardized format.

## Using annotation results

Annotation outputs can be used for:

- **exploratory analysis** – counting genes, inspecting interesting CDS,
- **comparative genomics** – clustering proteins from `.faa` files,
- **visualization** – loading `.gbk` or `.gff` into genome browsers,
- **downstream pipelines** – feeding `.gff` and `.fna` into other tools.

In this workshop, we focus on:

- understanding what Prokka did,
- identifying key outcome metrics,
- connecting the results back to the assembly used as input.

---

# Exercises

:::::::::::::::::::::::::::::::::::::::::::::: challenge

## Exercise: Run Prokka on your assembly

Assuming your assembly FASTA is in `assembly/`:

```bash
cd myproject/annotation
cp ../assembly/scaffolds.fasta sample01.scaffolds.fasta

prokka \
  --outdir sample01_prokka \
  --prefix sample01 \
  --addgenes \
  --locustag S01 \
  --increment 5 \
  --cpus 4 \
  --mincontiglen 1000 \
  sample01.scaffolds.fasta
```

**Questions:**

- Did Prokka complete without errors?
- How long did the run take?
- How many CDS, tRNAs, and rRNAs were predicted (check `sample01.txt`)?

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: challenge

## Exercise: Explore annotation files

From within `sample01_prokka`:

```bash
ls
head sample01.txt
head sample01.gff
head sample01.faa
```

**Questions:**

- What information is summarized in `sample01.txt`?
- How are features represented in the GFF file?
- What does a typical protein header in `sample01.faa` look like?

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: challenge

## Exercise: Genome vs metagenome mode

Discuss with a partner:

1. When would you use `--metagenome` with Prokka?
2. What kinds of datasets (e.g., bins, MAGs, entire metagenomes) might benefit from `--metagenome`?
3. For the assembly produced in this workshop, is `--metagenome` appropriate or not?

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: keypoints

- Prokka performs rapid, automated annotation of bacterial and archaeal genomes.
- You must provide an assembly FASTA file and specify sensible options (output directory, prefix, locus tag, CPUs, minimum contig length).
- Prokka generates many outputs; the most important include `.gff`, `.gbk`, `.faa`, `.ffn`, `.fna`, and `.txt`.
- Annotation results summarize genes, rRNAs, tRNAs, and other features, and can be used in downstream comparative and visualization workflows.
- The annotated genome is the culmination of the QC → trimming → assembly → annotation pipeline used in this workshop.

::::::::::::::::::::::::::::::::::::::::::::::::::
