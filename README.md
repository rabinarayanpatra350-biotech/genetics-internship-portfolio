# Genetics Assistant Internship — Complete Portfolio

**Rabi Narayan Patra** | yuvaintern.com | September–October 2026

A complete record of a five-week Genetics Assistant internship: five task submissions, each delivered as a
standalone report with its own repository, its own reproducibility bundle and its own verified results. This
repository is the index and narrative that ties them together.

---

## The five weeks at a glance

| Week | Task | Deliverable | Key verified result |
|---|---|---|---|
| **1** | Genetic Sequence Analysis and Reporting | 14-page report, 8 figures, 6 tables | A candidate marker recovered from a simulated cohort: **g.612C>G**, 6/6 cases vs 0/6 controls, Fisher p = 0.0022, survives Bonferroni |
| **2** | Experimental Design Simulation for Gene Expression Analysis | 15-page design report, 5 figures, 7 tables | A power analysis that justifies the sample size: **89% power** for a 2-fold change at n = 6, smallest detectable effect **1.83-fold** |
| **3** | Phylogenetic Analysis and Tree Reconstruction | 16-page report, 8 figures, 5 tables | A COX1 phylogeny of 12 vertebrates: primates **100%**, mammals **94%**, birds **100%**, fish **99%** bootstrap; human–chimpanzee **98.8%** identity |
| **4** | Automation of Genetic Data Analysis Pipeline | Working software: 12 modules, 86 tests, 17-page report | **genePipe** recovers a planted marker exactly and cuts a repeat run from **17.2 s to 0.0 s**; 11 defects found and fixed |
| **5** | Critical Review of Genetic Research Methods and Ethical Considerations | 31-page review, ~10,000 words, 7 figures, 64 references | A critical review with **seven documented case studies** and a fact-check ledger mapping every claim to its source |

Each week's repository is the **canonical submission** for that week and has been left untouched since it was
graded. The per-week repositories are:

| Week | Repository |
|---|---|
| 1 | [genetics-week1-sequence-analysis](https://github.com/rabinarayanpatra350-biotech/genetics-week1-sequence-analysis) |
| 2 | [genetics-week2-experimental-design](https://github.com/rabinarayanpatra350-biotech/genetics-week2-experimental-design) |
| 3 | [genetics-week3-phylogenetics](https://github.com/rabinarayanpatra350-biotech/genetics-week3-phylogenetics) |
| 4 | [genetics-week4-automation-pipeline](https://github.com/rabinarayanpatra350-biotech/genetics-week4-automation-pipeline) |
| 5 | [genetics-week5-elsi-critical-review](https://github.com/rabinarayanpatra350-biotech/genetics-week5-elsi-critical-review) |

---

## What the internship covered

The five tasks trace a deliberate arc from *doing* genetics to *designing* it, *reconstructing* it,
*automating* it, and finally *critically appraising* it:

**Week 1 — Doing the analysis.** A complete bioinformatics workflow on a self-designed, self-verifying
simulated gene (SIMG1, 1,500 bp, with a defined 5' UTR, a 1,299 bp CDS carrying a glycine-rich loop and a
catalytic DxxxxN motif, and a 3' UTR with a polyadenylation signal). Six documented steps — QC and six-frame
ORF detection, global Needleman–Wunsch alignment with exact variant calling, BLAST-style seed-and-extend
homology search, multiple sequence alignment with conservation profiling, substitution-spectrum analysis and
Fisher exact association testing with Bonferroni correction — found **81 variant calls at 13 sites** and one
candidate marker carried by all six cases and no controls.

**Week 2 — Designing the study before it exists.** A controlled RNA-seq experiment for hypoxia and
reoxygenation injury in endothelial cells: four arms × six biological replicates, four categories of control,
an explicit variable structure, a sample size justified by a negative-binomial power analysis rather than
convention, a randomisation plan verified to be unconfounded across batch, passage and operator, and
quantitative falsifiable predictions — including the counter-intuitive suppression of HIF1A mRNA during
hypoxia, which a naive design would misread as failure.

**Week 3 — Reconstructing evolutionary history from public data.** COX1 sequences for twelve vertebrate
species, retrieved from UniProt and NCBI, screened for taxonomic anomalies, aligned, and used to build
Neighbour-Joining and UPGMA trees with bootstrap support. The shallow clades are recovered with strong support
and the pairwise divergences match published values almost exactly. The deepest nodes are not resolved — and
the report **proves** this rather than hiding it, showing that all seven substitution models fail identically
and diagnosing why. It also documents a real data-quality failure: a GenBank record submitted as chicken COX1
proved **99.8% identical to human**.

**Week 4 — Automating the whole chain.** **genePipe**, a tested, resumable, configuration-driven
command-line pipeline that takes a FASTA file through cleaning, quality control, alignment, variant calling,
statistical association testing and phylogenetic reconstruction, and writes a documented run report. Twelve
modules, 86 automated tests, a stage cache, provenance capture and fail-safe orchestration. Run on a seeded
cohort it recovered the planted marker exactly; run unchanged on real public data it reproduced Week 3's
groupings. The report documents **eleven substantive defects** found and fixed during development — including
a DNA/protein alphabet collision that silently corrupted protein data and a cache that skipped work without
restoring state.

**Week 5 — Appraising the field.** A critical review of genetic research methods and their ethical, legal and
social implications, organised around four domains (the individual; the family and community; society and the
state; the human future) with seven documented case studies from HeLa (1951) to India's National Sickle Cell
Anaemia Elimination Mission (2025). Its organising argument is that **methodology and ethics are the same
question asked in two vocabularies**. Contested questions are presented with the strongest arguments on both
sides, and every quantitative claim is attributed to a source.

---

## Skills demonstrated across the five weeks

- **Sequence analysis**: alignment algorithms (global Needleman–Wunsch, progressive/star alignment), ORF
  detection and translation, variant calling, substitution spectra, transition/transversion analysis
- **Statistics**: Fisher's exact test and odds ratios, Benjamini–Hochberg false-discovery correction,
  negative-binomial power analysis, bootstrap resampling, multiple-testing discipline
- **Phylogenetics**: distance models (p-distance, Poisson, Kimura 2-parameter, BLOSUM62 and other
  amino-acid matrices), Neighbour-Joining and UPGMA reconstruction, clade support, saturation and molecular-clock
  diagnostics
- **Public data**: retrieval from NCBI E-utilities and the UniProt REST API, reference-identity screening,
  detection of mislabelled and anomalous records
- **Software engineering**: modular Python package design, argparse CLIs, layered configuration with
  validation, structured logging, stage caching, artefact-based state restoration, SHA-256 provenance, a
  86-test pytest suite, and an honest defect log
- **Critical appraisal**: literature synthesis, balanced treatment of contested ethical questions,
  regulatory analysis (international instruments and the Indian framework), and an evidence trail that maps
  every claim to its source

---

## Repository contents

```
├── README.md                    # this index
├── internship_overview.md       # narrative account of the whole internship
├── week1/                       # summary.md + verbatim submission_description.txt
├── week2/
├── week3/
├── week4/
└── week5/
```

Each `weekN/summary.md` records the task, the deliverable, the key verified results, the methods used and the
repository link. Each `weekN/submission_description.txt` is the **verbatim** description submitted through the
portal for that week.

The complete reports (DOCX and PDF), all figures and the reproducibility bundles for all five weeks are
attached to the [v1.0 release](../../releases/tag/v1.0) of this repository.

---

## Author

**Rabi Narayan Patra** — Genetics Assistant Intern, 2026.
GitHub: [@rabinarayanpatra350-biotech](https://github.com/rabinarayanpatra350-biotech)
