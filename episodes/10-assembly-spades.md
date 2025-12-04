---
title: Genome Assembly with SPAdes
teaching: 40
exercises: 20
---

:::::::::::::::::::::::::::::::::::::::::::::: questions

- How do we assemble microbial genomes from paired-end reads?
- How do we run SPAdes on the command line?
- What are the key SPAdes options we need to set (input files, threads, memory, output directory)?
- What files does SPAdes produce and which ones are most important?

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: objectives

- Describe the role of de novo assembly in microbial genomics.
- Run SPAdes on paired-end reads using appropriate options.
- Locate SPAdes output files (especially `contigs.fasta` and `scaffolds.fasta`).
- Perform a basic first inspection of the assembly output.
- Connect assembly results to later annotation with Prokka.

::::::::::::::::::::::::::::::::::::::::::::::::::

> This episode uses the microbial genome assembly activity you provided and adapts the
> SPAdes workflow for a Carpentries-style lesson. It assumes reads have already been
> organized, QC'd, and optionally trimmed in earlier episodes.

## What is genome assembly?

In **de novo genome assembly**, we reconstruct a genome from many short reads:

- Raw reads (FASTQ) → overlap / k-mer graph → contigs → scaffolds.
- For bacterial genomes, final sizes are often **2–6 Mb**.
- Assemblers like **SPAdes** are optimized for microbial genomes.

Our workflow:

1. Ensure reads are available in a project directory.
2. Run SPAdes with paired-end inputs.
3. Inspect key output files (especially the assembly FASTA).
4. Filter or post-process the assembly (covered here at a basic level).

## Setting up the assembly directory

Following the earlier project structure, we will work in the `assembly/` directory:

```bash
cd myproject
cd assembly
pwd
```

You should see that your **current working directory** is `.../myproject/assembly`.

Make sure your reads are accessible, for example:

- `../trimmed/sample01_R1.trimmed.fastq.gz`
- `../trimmed/sample01_R2.trimmed.fastq.gz`

or, if trimming was skipped in this run:

- `../raw_reads/sample01_R1.fastq.gz`
- `../raw_reads/sample01_R2.fastq.gz`

## Running SPAdes

SPAdes is run with a command that specifies:

- `-1` – path to R1 FASTQ,
- `-2` – path to R2 FASTQ,
- `--threads` – number of CPU cores,
- `--memory` – maximum RAM (in GB),
- `-k` – list of k-mer sizes,
- `-o` – output directory.

A typical command, adapted from your assembly activity, looks like:

```bash
spades.py \
  -1 ../raw_reads/ERR435025_R1.fastq.gz \
  -2 ../raw_reads/ERR435025_R2.fastq.gz \
  --threads 10 \
  --memory 120 \
  -k 21,33,55,77,99,127 \
  -o ERR435025_assembly
```

Adjust:

- input paths (`-1`, `-2`) to match your dataset,
- `--threads` based on the number of cores available,
- `--memory` based on server limits,
- `-k` if needed (these k-mers are typical for Illumina reads).

:::::::::::::::::::::::::::::::::::::::::::::: callout

### Running SPAdes in a long session

Genome assembly can take **many minutes to hours**, depending on:

- read depth,
- genome size,
- server load,
- number of threads and memory.

On shared systems, it is common to run SPAdes inside a session manager like `screen`
or `tmux` so that the process keeps running even if your SSH connection drops.

Your instructor may demonstrate this, or the run may be pre-computed.

::::::::::::::::::::::::::::::::::::::::::::::::::

## Inspecting SPAdes output

Once SPAdes finishes, you should have an output directory (for example `ERR435025_assembly/`):

```bash
ls ERR435025_assembly
```

Common files and directories include:

- `contigs.fasta` – assembled contigs
- `scaffolds.fasta` – assembled scaffolds (contigs linked by paired-end information)
- `spades.log` – log file describing the run
- `params.txt` – parameters used
- other intermediate files and reports

We will usually use **`scaffolds.fasta`** (or sometimes `contigs.fasta`) as the input for downstream steps.

Copy the scaffold file into a convenient location:

```bash
cp ERR435025_assembly/scaffolds.fasta .
ls
```

You should now see `scaffolds.fasta` in your `assembly/` directory.

## First look at the assembly

Use commands from earlier Unix episodes to inspect the assembly:

```bash
head scaffolds.fasta
grep -c '^>' scaffolds.fasta
```

- `head` shows the first few contigs.
- `grep -c '^>'` counts how many contigs are present (each header starts with `>`).

If helper scripts are available (as in your assembly notes), you can compute stats such as:

```bash
seqstat scaffolds.fasta
N50_count.pl scaffolds.fasta
```

These provide:

- total assembly length,
- number of contigs,
- N50 (a measure of contig length distribution).

Later, you may want to filter contigs by length (for example keeping only those ≥ 1,000 bp) before annotation, but the basic SPAdes assembly output is already enough to proceed to Prokka.

---

# Exercises

:::::::::::::::::::::::::::::::::::::::::::::: challenge

## Exercise: Run SPAdes (or examine a prepared run)

If computing resources allow, run SPAdes on your sample:

```bash
cd myproject/assembly

spades.py \
  -1 ../raw_reads/sample01_R1.fastq.gz \
  -2 ../raw_reads/sample01_R2.fastq.gz \
  --threads 8 \
  --memory 32 \
  -k 21,33,55,77,99,127 \
  -o sample01_assembly
```

If SPAdes has been pre-run for you, skip directly to examining the output directory.

**Questions:**

- How long did the run take?
- Did SPAdes report any warnings or errors in `spades.log`?

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: challenge

## Exercise: Count contigs and inspect the assembly

After SPAdes finishes (or using a provided assembly):

```bash
cd myproject/assembly
cp sample01_assembly/scaffolds.fasta .
grep -c '^>' scaffolds.fasta
head scaffolds.fasta
```

**Questions:**

- How many contigs are present?
- What does the first header line look like?
- How might you identify the length of a specific contig?

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: challenge

## Exercise: Think ahead to annotation

Discuss with a partner:

1. Why might we want to filter out very short contigs before annotation?
2. Which file from the SPAdes output will we give to Prokka in the next episode?
3. What information about the assembly might be important to record in your project metadata?

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: keypoints

- SPAdes performs de novo genome assembly from paired-end reads.
- You must provide paths to R1 and R2 reads, thread count, memory limit, and an output directory.
- SPAdes produces many files; `contigs.fasta` and `scaffolds.fasta` are the most important for downstream analysis.
- Basic inspection of the assembly (number of contigs, total size, N50) helps assess quality.
- The assembly FASTA file will be the input to Prokka for genome annotation.

::::::::::::::::::::::::::::::::::::::::::::::::::
