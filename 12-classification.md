---
title: Taxonomic Classification with the Genome Taxonomy Database (GTDB)
teaching: 25
exercises: 20
---

:::::::::::::::::::::::::::::::::::::::::::::: questions

- How can we classify a microbial genome using a standardized taxonomy?
- What is the Genome Taxonomy Database (GTDB), and why is it widely used?
- How do we use GTDB-Tk to assign taxonomy to an assembled genome?
- How does classification complete the workflow from raw reads → assembly → annotation?

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: objectives

- Understand the purpose of GTDB and genome-based taxonomy.
- Run a GTDB-Tk classification workflow on a SPAdes-assembled genome.
- Interpret GTDB output files, including `classification.tsv` and marker summaries.
- Connect taxonomic assignments to biological interpretation and downstream comparison.

::::::::::::::::::::::::::::::::::::::::::::::::::

> In this final episode, learners extend the microbial genomics workflow by adding
> **taxonomic classification** of the assembled genome using the Genome Taxonomy Database (GTDB).

## What is GTDB?

The **Genome Taxonomy Database (GTDB)** provides a standardized taxonomy for bacteria and archaea based on whole-genome phylogenies.

GTDB:

- uses phylogenomic marker sets (120 markers for bacteria, 122 for archaea),
- updates taxonomy regularly with high-quality genomes,
- replaces inconsistent or outdated NCBI classifications,
- enables reproducible, genome-based comparisons across studies.

## Inputs for GTDB-Tk

GTDB-Tk requires:

- an assembled genome FASTA file (typically `contigs.fasta` from SPAdes),
- access to GTDB reference databases (large; installed by the instructor),
- sufficient CPU and RAM (usually ≥ 4 CPUs, ≥ 16 GB RAM).

Your assembled genome from Episode 10:

```
assembly/sample01_spades/contigs.fasta
```

## Running GTDB-Tk

Create a taxonomy output directory:

```bash
mkdir -p taxonomy
```

Run the GTDB classification workflow:

```bash
gtdbtk classify_wf   --genome_dir assembly/sample01_spades   --out_dir taxonomy/sample01_gtdb   --cpus 4
```

GTDB-Tk will:

1. identify marker genes in the genome,
2. compare them to GTDB reference markers,
3. place the genome within a reference tree,
4. assign a GTDB taxonomy.

:::::::::::::::::::::::::::::::::::::::::::::: callout

### Database requirements

GTDB-Tk requires access to a ~60–100 GB database that your instructor will provide.  
Learners do **not** download this themselves.  
Ask instructors for the database path if needed.

::::::::::::::::::::::::::::::::::::::::::::::::::

## GTDB-Tk output files

In `taxonomy/sample01_gtdb/`, you will find:

### **`classification.tsv`**
Contains final taxonomic assignment:

```
sample01    d__Bacteria; p__Firmicutes; c__Bacilli; o__Bacillales; f__Bacillaceae; g__Bacillus; s__Bacillus subtilis
```

### **Marker summaries**
- `markers_summary.tsv` — marker presence, completeness, contamination indicators  
- `gtdbtk.bac120.classify.tree` — placement tree for bacteria  
- `gtdbtk.ar122.classify.tree` — placement tree for archaea (if applicable)

### **Logs and intermediate files**

Useful for troubleshooting completeness and contamination issues.

## Connecting classification to the workflow

You have now completed the full microbial genomics workflow:

1. **Raw reads**
2. **QC (FastQC)**
3. **Trimming**
4. **Assembly (SPAdes)**
5. **Annotation (Prokka)**
6. **Classification (GTDB-Tk)** ← *This episode*

Taxonomic classification enables:

- determining the organism’s closest known relatives,
- contextualizing functional annotation,
- identifying potential contamination,
- comparing genomes across studies or timepoints.

---

# Exercises

:::::::::::::::::::::::::::::::::::::::::::::: challenge

## Exercise: View your GTDB classification

```bash
less taxonomy/sample01_gtdb/classification.tsv
```

**Questions:**

- What genus and species did Prokka predict?
- Does the GTDB assignment align with annotation results?

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: challenge

## Exercise: Marker completeness

```bash
less taxonomy/sample01_gtdb/markers_summary.tsv
```

**Questions:**

- How many marker genes were detected?
- Do completeness and contamination metrics look reasonable?

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: challenge

## Exercise: Biological interpretation

Discuss:

- What ecological or metabolic traits are associated with this clade?
- Are there related genomes you could compare with in future analyses?
- How could GTDB classification inform experimental hypotheses?

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: keypoints

- GTDB provides a standardized genome-based taxonomy for bacteria and archaea.
- GTDB-Tk classifies genomes using phylogenomic markers and reference trees.
- `classification.tsv` is the key file containing the taxonomic assignment.
- Classification adds biological context and completes the raw → annotated → classified workflow.
- Proper project structure keeps classification outputs organized and reproducible.

::::::::::::::::::::::::::::::::::::::::::::::::::
