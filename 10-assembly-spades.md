---
title: Genome Assembly with SPAdes
teaching: 30
exercises: 25
---

:::::::::::::::::::::::::::::::::::::::::::::: questions

- What does *de novo* genome assembly do with our trimmed reads?
- How do we run SPAdes on a remote server using paired-end Illumina data?
- Where does SPAdes write its outputs, and which files matter for downstream analysis?
- How can we read basic assembly statistics (number of contigs, total length, N50)?

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: objectives

- Explain at a high level how *de novo* assembly reconstructs a genome from reads.
- Run SPAdes on trimmed paired-end reads in a reproducible project structure.
- Locate and interpret key SPAdes output files (logs, `contigs.fasta`, `scaffolds.fasta`).
- Extract and interpret simple assembly metrics that will inform annotation with Prokka.

::::::::::::::::::::::::::::::::::::::::::::::::::

> This episode is adapted from the SPAdes assembly workflow materials and the genome
> assembly lecture, with a focus on running a small *de novo* assembly on a shared server.

## What is *de novo* assembly?

In this workshop we **do not** map reads to a reference genome.  
Instead, we run a *de novo* assembly:

- Reads are broken into **k-mers** (short overlapping words).
- A **graph** is built that represents how k-mers connect.
- The assembler walks the graph to reconstruct **contigs** (continuous sequences).
- Contigs may then be linked into **scaffolds** when paired-end information supports it.

Key terms:

- **Contig** – a continuous assembled sequence with no gaps (Ns).
- **Scaffold** – a sequence that may contain gaps (Ns) where contigs are linked.
- **Coverage** – average number of reads covering each base.
- **N50** – a length such that 50% of the assembled bases are in contigs of this length or longer.

We will assemble our **trimmed reads** from Episode 9 into contigs using SPAdes.

## Inputs and outputs for SPAdes

We assume the following project structure from earlier episodes:

```text
myproject/
├── metadata/
├── raw_reads/
├── qc/
├── trimmed/
├── assembly/
├── annotation/
└── scripts/
```

For a single sample (`sample01`), you should have trimmed reads in:

```text
trimmed/sample01_R1.trimmed.fastq.gz
trimmed/sample01_R2.trimmed.fastq.gz
```

SPAdes will create a **new directory** inside `assembly/`, for example:

```text
assembly/sample01_spades/
```

This contains:

- `contigs.fasta` – assembled contigs (main file we will use for annotation)
- `scaffolds.fasta` – scaffolds; may contain Ns
- `assembly_graph.fastg` – graph representation of the assembly
- `spades.log` – log file with parameters and progress
- `params.txt` – summary of command-line options used

Keeping the output in `assembly/` helps maintain a tidy, reproducible project.

## Running SPAdes

Change into your project directory:

```bash
cd ~/myproject
```

Create an output directory name (SPAdes will create it):

```bash
mkdir -p assembly
```

Run SPAdes with paired-end trimmed reads:

```bash
spades.py   -1 trimmed/sample01_R1.trimmed.fastq.gz   -2 trimmed/sample01_R2.trimmed.fastq.gz   -o assembly/sample01_spades   --threads 4   --memory 16
```

Options:

- `-1`, `-2` – forward and reverse reads
- `-o` – output directory
- `--threads` – number of CPU threads to use
- `--memory` – maximum RAM (in GB) to use

Ask your instructor how many threads and how much memory are appropriate for your server.

:::::::::::::::::::::::::::::::::::::::::::::: callout

## Running SPAdes takes time

Even on a small dataset, SPAdes can take **several minutes**.  
On larger genomes, or with many samples, assemblies may take **hours**.

- Do **not** run SPAdes on a login node if your system uses a scheduler.
- Make sure you understand where outputs are going before you start.

::::::::::::::::::::::::::::::::::::::::::::::::::

## Inspecting the SPAdes output

When SPAdes finishes, list the output directory:

```bash
ls assembly/sample01_spades
```

You should see files including:

- `contigs.fasta`
- `scaffolds.fasta`
- `spades.log`
- `params.txt`

The main file we will use for annotation is:

```bash
assembly/sample01_spades/contigs.fasta
```

We can quickly inspect it:

```bash
head assembly/sample01_spades/contigs.fasta
```

Each contig starts with a header line:

```text
>NODE_1_length_48231_cov_38.7
```

This contains:

- a contig ID (`NODE_1`)
- its length in base pairs (`length_48231`)
- estimated coverage (`cov_38.7`)

## Simple assembly statistics

We can get basic stats from the contigs file.

Count contigs:

```bash
grep -c "^>" assembly/sample01_spades/contigs.fasta
```

Estimate total assembly length (requires `seqkit`):

```bash
seqkit stats assembly/sample01_spades/contigs.fasta
```

Example output might include:

```text
file                              format  type  num_seqs  sum_len  min_len  avg_len  max_len
assembly/sample01_spades/contigs.fasta  FASTA  DNA      143     4.8e6    500      33706    182431
```

This tells you:

- **num_seqs** – number of contigs
- **sum_len** – total assembled length (approx genome size)
- **max_len** – length of the longest contig

N50 is also reported in some tools or logs, but even these three numbers already give a sense of assembly quality.

:::::::::::::::::::::::::::::::::::::::::::::: callout

## Interpreting assembly quality

Very roughly:

- If total length is close to the expected genome size → good coverage.
- If there are *very many* short contigs → assembly may be fragmented.
- A few long contigs with reasonable coverage values → more contiguous assembly.

We will not perfect the assembly in this workshop, but we will generate a reasonable draft for annotation.

::::::::::::::::::::::::::::::::::::::::::::::::::

## Preparing for annotation

Prokka (Episode 11) will take the assembled contigs as input.  
For example:

```bash
prokka --outdir annotation/sample01_prokka        --prefix sample01        assembly/sample01_spades/contigs.fasta
```

So the **main output** of SPAdes to remember is:

```text
assembly/sample01_spades/contigs.fasta
```

Make sure you know:

- where it lives,
- how large it is,
- how many contigs it contains.

These details will be useful when interpreting annotation results.

---

# Exercises

:::::::::::::::::::::::::::::::::::::::::::::: challenge

## Exercise: Identify inputs and outputs for SPAdes

From your project directory, run:

```bash
ls trimmed
ls assembly
```

**Questions:**

- Which files in `trimmed/` should be used as SPAdes inputs?
- What will the SPAdes output directory be called for `sample01`?

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: challenge

## Exercise: Construct a SPAdes command

Write down a complete SPAdes command using:

- `trimmed/sample01_R1.trimmed.fastq.gz`
- `trimmed/sample01_R2.trimmed.fastq.gz`
- output directory `assembly/sample01_spades`
- 4 threads and 16 GB of memory

Compare your command with a neighbor or with the instructor’s example.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: challenge

## Exercise: Explore the assembly directory

After SPAdes has finished (or using a pre-computed result):

```bash
ls assembly/sample01_spades
```

**Questions:**

- Which files look most important for downstream analysis?
- Where is the `contigs.fasta` file located?
- What other information is captured in `spades.log` or `params.txt`?

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: challenge

## Exercise: Basic assembly stats

Using the assembled contigs:

```bash
grep -c "^>" assembly/sample01_spades/contigs.fasta
seqkit stats assembly/sample01_spades/contigs.fasta
```

**Questions:**

- How many contigs are there?
- What is the total assembled length?
- How does this compare to the expected genome size?

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: keypoints

- *De novo* assembly reconstructs a genome from overlapping reads, producing contigs and scaffolds.
- SPAdes uses paired-end trimmed reads as input and writes outputs to an assembly directory.
- `contigs.fasta` is the key file for downstream annotation with Prokka.
- Simple statistics (number of contigs, total length, max length) help assess assembly quality.
- Keeping assembly outputs in a dedicated `assembly/` directory supports a tidy, reproducible workflow.

::::::::::::::::::::::::::::::::::::::::::::::::::
