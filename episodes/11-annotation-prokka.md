---
title: Genome Annotation with Prokka
teaching: 30
exercises: 20
---

:::::::::::::::::::::::::::::::::::::::::::::: questions

- What is genome annotation, and why do we perform it after assembly?
- How do we run Prokka on an assembled microbial genome?
- What do Prokka’s output files contain?
- How does annotation fit into the full workflow from raw reads → assembly → biological interpretation?

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: objectives

- Explain the purpose of microbial genome annotation.
- Run Prokka on an assembled genome using reproducible project organization.
- Identify and interpret key annotation outputs (`.gff`, `.gbk`, `.faa`, `.ffn`, `.txt`).
- Understand how Prokka uses contigs to predict genes, proteins, and RNA features.
- Prepare annotated files for downstream exploration or comparative genomics.

::::::::::::::::::::::::::::::::::::::::::::::::::

> In this final episode, learners annotate the genome assembled in Episode 10.
> Prokka identifies coding sequences (CDS), rRNAs, tRNAs, and other features, producing files
> suitable for exploration, visualization, or comparative genomics.

## What is genome annotation?

Genome annotation assigns biological meaning to assembled sequences.

Prokka identifies:

- **protein‑coding genes (CDS)**
- **tRNAs and rRNAs**
- **signal peptides**
- **functional annotations** (based on databases)

Annotation answers biological questions such as:

- How many genes are present?
- What pathways or functions might the organism have?
- Are there mobile elements or phage regions?

## Inputs and outputs

Prokka requires one main input:

```
assembly/sample01_spades/contigs.fasta
```

This is the cleaned, assembled genome from SPAdes.

Prokka outputs many files in a dedicated directory:

- `sample01.gff` — combined annotation + sequence
- `sample01.gbk` — GenBank format (useful for visualization)
- `sample01.faa` — predicted protein sequences
- `sample01.ffn` — nucleotide sequences of CDS
- `sample01.fna` — contig sequences
- `sample01.tbl` — feature table
- `sample01.txt` — summary statistics

Keeping these in `annotation/` supports reproducibility and tidy organization.

## Running Prokka

Navigate to your project directory:

```bash
cd ~/myproject
```

Run Prokka on your assembled contigs:

```bash
prokka   --outdir annotation/sample01_prokka   --prefix sample01   --cpus 4   --locustag S01   --addgenes   --mincontiglen 200   assembly/sample01_spades/contigs.fasta
```

Options used:

- `--outdir` — directory for results
- `--prefix` — prefix for output filenames
- `--cpus` — number of CPU threads
- `--locustag` — prefix for gene IDs
- `--addgenes` — adds gene features for each CDS
- `--mincontiglen` — ignore very short contigs

:::::::::::::::::::::::::::::::::::::::::::::: callout

## Prokka and reproducibility

Prokka reports:

- exact parameters used,
- software versions,
- database versions,

which is critical for reproducible microbial genomics workflows.

::::::::::::::::::::::::::::::::::::::::::::::::::

## Inspecting annotation outputs

List results:

```bash
ls annotation/sample01_prokka
```

Start with the summary:

```bash
less annotation/sample01_prokka/sample01.txt
```

Look for:

- total CDS
- number of tRNAs and rRNAs
- contig counts
- annotation completeness

Explore protein sequences:

```bash
less annotation/sample01_prokka/sample01.faa
```

Explore the GFF file:

```bash
less annotation/sample01_prokka/sample01.gff
```

This file contains all annotated features along with coordinates and metadata.

## Connecting annotation to the workflow

You have now completed the pipeline:

1. **Raw reads**  
2. **QC (FastQC)**  
3. **Trimming**  
4. **Assembly (SPAdes)**  
5. **Annotation (Prokka)**  

Prokka’s outputs can be used for:

- exploring gene functions,
- identifying potential pathways,
- comparing genomes,
- visualizing features in genome browsers.

---

# Exercises

:::::::::::::::::::::::::::::::::::::::::::::: challenge

## Exercise: Run Prokka (or inspect a pre-computed run)

Run:

```bash
prokka --outdir annotation/sample01_prokka        --prefix sample01        assembly/sample01_spades/contigs.fasta
```

**Questions:**

- How long did it take?
- How many CDS, tRNAs, and rRNAs were identified?

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: challenge

## Exercise: Explore annotation files

```bash
less annotation/sample01_prokka/sample01.txt
less annotation/sample01_prokka/sample01.gff
less annotation/sample01_prokka/sample01.faa
```

**Questions:**

- What does the summary (`.txt`) reveal?
- What kinds of features appear in the `.gff` file?
- How are protein IDs represented in `.faa`?

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: challenge

## Exercise: Advanced thinking (optional)

Discuss:

- Why might different annotation tools give different gene counts?
- How could you incorporate annotation results into comparative genomics?
- What additional analyses might follow annotation?

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: keypoints

- Prokka provides rapid, standardized annotation for bacterial genomes.
- Its outputs include GFF, GBK, FAA, FFN, and summary files.
- The annotation step completes the pipeline from raw reads to curated genome features.
- Good project organization ensures annotation results remain traceable and reproducible.

::::::::::::::::::::::::::::::::::::::::::::::::::
