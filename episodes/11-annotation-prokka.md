---
title: Genome Annotation with Prokka
teaching: 25
exercises: 15
---

Identify:
- coding sequences (CDS)
- rRNA / tRNA
- functional annotations

Run:
```bash
prokka  --outdir annotation/sample  --prefix sample  assembly/spades_output/contigs.fasta
```

Outputs:
- sample.gff
- sample.faa
- sample.ffn

:::::::::::::::::::::::::::::::::::::::: keypoints

- Prokka provides rapid microbial gene prediction.

::::::::::::::::::::::::::::::::::::::::::::::::::
