---
title: De Novo Assembly with SPAdes
teaching: 25
exercises: 20
---

:::::::::::::::::::::::::::::::::::::::::::::: questions

- How do short reads become longer contigs in an assembly?
- What are contigs, scaffolds, and N50?
- How do we run SPAdes on the rampers server using trimmed reads?
- How can we quickly inspect the assembly output?

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: objectives

- Describe at a high level how de novo assembly reconstructs genomes from reads.
- Define contigs, scaffolds, and N50 in the context of assemblies.
- Run SPAdes on trimmed paired-end reads to generate an assembly.
- Inspect the resulting `contigs.fasta` file and basic assembly statistics.

::::::::::::::::::::::::::::::::::::::::::::::::::

> This episode is adapted from short microbial assembly teaching materials and
> the SPAdes documentation, customized for the rampers server project layout.

## From reads to contigs

Illumina reads are typically 100–300 bases long, while microbial genomes have
millions of bases. An **assembler**:

- finds overlaps between reads,
- builds a graph of how reads connect,
- collapses paths through that graph into longer sequences called **contigs**.

Key terms:

- **contig** – a contiguous stretch of assembled sequence.
- **scaffold** – a set of contigs ordered and oriented with gaps (Ns) between
  them.
- **N50** – the contig length such that 50% of the assembly lies in contigs of
  that length or longer.

Larger N50 and fewer contigs usually mean a more contiguous assembly, but
context (genome size, repeats, coverage) matters.

## In-person assembly activity (offline)

Before running SPAdes, we will do a **paper-based assembly**:

- You will receive strips of paper with short “reads” from a simple story.
- Your task is to find overlaps and reconstruct the original story.
- You will notice challenges like repeats and ambiguous joins.

This activity builds intuition for what assemblies are doing behind the scenes.

## Running SPAdes on the rampers server

We will run SPAdes using the trimmed reads in `data/trimmed/` and write all
output to an `assembly/` directory.

From your project root:

```bash
cd ~/microbial_project
mkdir -p assembly

spades.py   -1 data/trimmed/sample_R1.trimmed.fastq.gz   -2 data/trimmed/sample_R2.trimmed.fastq.gz   -o assembly/spades_sample
```

Notes:

- `-1` and `-2` specify the paired-end read files.
- `-o` sets the output directory.
- SPAdes may take several minutes depending on data size and server load.

Your instructor may provide a script that runs SPAdes with the correct sample
names for the workshop dataset.

## Inspecting `contigs.fasta`

When SPAdes finishes, list the output directory:

```bash
ls assembly/spades_sample
```

You should see files including `contigs.fasta` and `scaffolds.fasta` (we will
focus on `contigs.fasta`).

To count the number of contigs:

```bash
grep -c "^>" assembly/spades_sample/contigs.fasta
```

To look at the first contig:

```bash
head -n 20 assembly/spades_sample/contigs.fasta
```

If `seqkit` is available on the rampers server, we can get quick stats:

```bash
seqkit stats assembly/spades_sample/contigs.fasta
```

This will report total length, N50, and other metrics. Compare the total length
to the expected genome size for the organism.

If `seqkit` is not available, your instructor may provide precomputed assembly
statistics for discussion.

:::::::::::::::::::::::::::::::::::::::::::::: challenge

## Exercise: Interpreting assembly metrics

Using the stats shown by your instructor (or from `seqkit stats`), answer:

1. Approximately how large is the assembly (total length)?
2. How many contigs are there?
3. What is the N50 value?
4. Does the total length seem reasonable for a microbial genome of this type?

Discuss whether you would consider this assembly “good enough” for basic
annotation.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::: keypoints

- Assemblers like SPAdes reconstruct genomes from overlapping short reads,
  producing **contigs**.
- N50 summarizes assembly contiguity: larger N50 usually means a more contiguous
  assembly.
- We run SPAdes on trimmed reads and store outputs in `assembly/`.
- `contigs.fasta` is the main file we use for downstream annotation.

::::::::::::::::::::::::::::::::::::::::::::::::::
