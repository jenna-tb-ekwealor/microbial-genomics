---
title: Trimming Reads (fastp)
teaching: 15
exercises: 10
---

```bash
fastp  -i data/raw/sample_R1.fastq.gz  -I data/raw/sample_R2.fastq.gz  -o data/trimmed/sample_R1.trimmed.fastq.gz  -O data/trimmed/sample_R2.trimmed.fastq.gz
```

::::::::::::::::::::::::::::::::::::::: keypoints

- Clean reads produce better assemblies.

::::::::::::::::::::::::::::::::::::::::::::::::::
