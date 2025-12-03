---
title: Assessing Read Quality (FastQC)
teaching: 20
exercises: 10
---

Run:
```bash
fastqc data/raw/*.fastq.gz -o qc
```

Inspect quality, adapters, overrepresented sequences.

::::::::::::::::::::::::::::::::::::::: keypoints

- QC identifies problems before trimming.

::::::::::::::::::::::::::::::::::::::::::::::::::
