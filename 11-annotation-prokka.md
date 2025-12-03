---
title: Genome Annotation with Prokka
teaching: 25
exercises: 15
---

:::::::::::::::::::::::::::::::::::::::::::::: questions

- What does it mean to "annotate" a genome?
- What features does Prokka predict from an assembled microbial genome?
- How do we run Prokka on the contigs from SPAdes?
- What useful information is stored in the GFF and FAA files?

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: objectives

- Explain the goal of genome annotation in microbial genomics.
- Run Prokka on an assembled genome to predict genes and other features.
- Identify key output files from Prokka (GFF, FAA, FFN, etc.).
- Perform simple inspections of annotation results on the rampers server.

::::::::::::::::::::::::::::::::::::::::::::::::::

> This episode is adapted from short microbial annotation teaching materials
> and the Prokka documentation.

## What is genome annotation?

An assembly (like `contigs.fasta`) is just raw sequence. **Annotation** adds
biological meaning by predicting:

- protein-coding genes (CDS),
- rRNA and tRNA genes,
- product names and functional descriptions (where possible).

Prokka is a rapid annotation pipeline tuned for **bacterial, archaeal, and
viral** genomes.

## Inputs and outputs of Prokka

**Input:**

- a FASTA file with assembled contigs (e.g. `contigs.fasta`).

**Outputs (in an output directory):**

- `*.gff` – combined sequence and annotation in one file.
- `*.faa` – amino acid sequences of predicted proteins.
- `*.ffn` – nucleotide sequences of predicted genes.
- `*.tbl` – feature table.
- `*.txt` – summary of the run.

These files can be used for downstream analysis (e.g. searching for particular
genes, comparing annotations, building phylogenies).

## Running Prokka on the rampers server

We will annotate the SPAdes contigs produced in the previous episode.

From your project root:

```bash
cd ~/microbial_project
mkdir -p annotation

prokka   --outdir annotation/sample   --prefix sample   assembly/spades_sample/contigs.fasta
```

Options used:

- `--outdir` – where to put the output files.
- `--prefix` – prefix for output filenames.
- the final argument is the input FASTA file.

Prokka will print progress messages and may take a few minutes depending on the
size of the assembly and the server load.

After it finishes, list the outputs:

```bash
ls annotation/sample
```

Look for `sample.gff`, `sample.faa`, and `sample.txt`.

## Inspecting annotation results

To get a quick sense of what Prokka found:

```bash
grep -c "	CDS	" annotation/sample/sample.gff
```

This counts how many CDS features were annotated.

You can also inspect the summary file:

```bash
less annotation/sample/sample.txt
```

Look for lines describing:

- the number of contigs and bases,
- the number of CDS, rRNA, tRNA predictions,
- the annotation databases used.

To preview protein sequences:

```bash
head annotation/sample/sample.faa
```

Each entry has a header line with the locus tag and product name (if any),
followed by the amino acid sequence.

:::::::::::::::::::::::::::::::::::::::::::::: challenge

## Exercise: Exploring Prokka output

Using `sample.gff` and `sample.faa`, try to answer:

1. Approximately how many protein-coding genes were predicted?
2. Can you find a gene annotated as something like "DNA gyrase" or another
   familiar function?
3. How might you extract all protein sequences for a particular functional
   category (conceptually)?

Discuss how you might use these files in a downstream analysis (e.g. searching
for specific genes, building a phylogenetic tree).

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: keypoints

## Key Points

- Annotation adds biological meaning to an assembly by predicting genes and
  other features.
- Prokka is a rapid pipeline for annotating microbial genomes.
- Key outputs include GFF (features + coordinates) and FAA (protein sequences).
- We run Prokka on `contigs.fasta` from SPAdes and store results in
  `annotation/` for downstream analysis.

::::::::::::::::::::::::::::::::::::::::::::::::::
