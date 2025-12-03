---
title: De Novo Assembly with SPAdes
teaching: 25
exercises: 20
---

## What is assembly?
Short reads → contigs → scaffolds  
Terms:
- contig
- N50

## In-person assembly activity (offline)
You will assemble a “genome” from paper fragments to simulate contig construction
before using SPAdes.

## Running SPAdes
```bash
spades.py  -1 data/trimmed/sample_R1.trimmed.fastq.gz  -2 data/trimmed/sample_R2.trimmed.fastq.gz  -o assembly/spades_output
```

Inspect:
```bash
less assembly/spades_output/contigs.fasta
grep -c "^>" assembly/spades_output/contigs.fasta
```

::::::::::::::::::::::::::::::::::::::: keypoints

- SPAdes assembles reads into contigs.
- Inspect contigs and compute N50.

::::::::::::::::::::::::::::::::::::::::::::::::::
