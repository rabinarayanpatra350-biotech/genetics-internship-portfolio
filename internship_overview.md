# Internship Overview

**Genetics Assistant Internship** | Rabi Narayan Patra | yuvaintern.com | September–October 2026

This document is the narrative record of the internship: what each week asked for, what was produced, what the
results actually showed, and what the five weeks collectively demonstrate.

---

## 1. The shape of the internship

The five tasks were not five unrelated assignments. Read in order, they trace the full life of a genetic
research project: an analysis is performed (Week 1), a study is designed (Week 2), evolutionary history is
reconstructed from public data (Week 3), the analysis chain is automated into software (Week 4), and finally
the field itself is critically appraised together with its ethical, legal and social implications (Week 5).

That arc is worth naming because it means the later weeks could build on the earlier ones — and they do.
The variant-calling logic written by hand in Week 1 reappears as a module in the Week 4 pipeline. The
phylogenetic distances implemented for Week 3 are re-used by that pipeline and reproduce Week 3's groupings
when it is run on the same public data. The power analysis in Week 2 is the same statistical reasoning that
Week 4 encodes as an automated stage. And the ethical questions raised in Week 5 are the questions that
Week 2's design decisions — what to measure, whom to sample, what to promise — were already answering
implicitly.

A recurring theme emerged across all five weeks: **the honest report of a limitation is worth more than a
confident result that the data cannot support.** In Week 3 this meant proving that seven substitution models
all fail at the deepest nodes rather than drawing a tree the evidence did not justify. In Week 4 it meant
documenting eleven defects that would otherwise have produced output which *looked* correct. In Week 5 it
meant reporting the range of published estimates for the ancestry gap rather than the most convenient figure.
This was not a stylistic preference; in each case the honest version was also the more useful one.

---

## 2. Week-by-week record

### Week 1 — Genetic Sequence Analysis and Reporting

**Task.** Conduct a bioinformatics analysis of genetic sequence data: design or obtain a dataset, analyse it,
and report the findings with full documentation.

**Approach.** Rather than analyse an arbitrary public sequence, I designed a **self-verifying simulated
dataset** so that the analysis could be checked against a known ground truth. The simulated gene SIMG1 is
1,500 bp with a defined architecture: a 5' UTR, a 1,299 bp coding sequence carrying a glycine-rich loop and a
catalytic DxxxxN motif, and a 3' UTR with a polyadenylation signal. Twelve sample sequences were derived from
it — six cases and six controls — with a documented catalogue of substitutions, in-frame deletions, two
premature-stop variants and a frameshift, all generated from a fixed random seed. The simulation script
asserts every designed effect after construction, so the dataset verifies itself.

**Method.** Six documented pipeline steps: quality control and six-frame ORF detection; global
Needleman–Wunsch alignment with exact variant calling and functional annotation; BLAST-style seed-and-extend
homology search against a four-sequence database; multiple sequence alignment with conservation profiling and
an enrichment test; substitution-spectrum analysis; and Fisher exact association testing with Bonferroni
correction.

**Results.** **81 variant calls at 13 sites** (74 SNVs, 6 deletions, 1 insertion); transition/transversion
ratio **2.36**; 830 of 1,500 alignment positions conserved. One variant — the missense substitution
**g.612C>G (P171R)** — was carried by **all six cases and no controls** (Fisher p = 0.0022) and survived
Bonferroni correction, making it the leading candidate marker. Three loss-of-function variants truncated the
protein to 39, 42 and 404 residues.

**Deliverable.** A 14-page report (~3,828 words, 6 tables, 8 figures including annotated console and
alignment-viewer screenshots), a 232-word portal description, and a reproducibility bundle of 55 files.
Repository: `genetics-week1-sequence-analysis`.

---

### Week 2 — Experimental Design Simulation for Gene Expression Analysis

**Task.** Design an experiment for gene expression analysis: choose the methodology, justify it, and set out
the full procedure, expected results and analysis plan.

**Approach.** A controlled RNA-seq study of **hypoxia and reoxygenation injury in human endothelial cells**,
with orthogonal qRT-PCR validation. Four arms — normoxia, hypoxia, hypoxia with reoxygenation, and hypoxia
with HIF1A knockdown — of six biological replicates each, four categories of control, an explicit variable
structure separating controlled from confounding factors, and randomisation balanced across three processing
batches, two cell passages and two operators.

**Method.** The design decisions that are usually asserted were **computed instead**. Sample size came from a
negative-binomial power analysis (Hart et al. 2013), and the randomisation plan was generated
programmatically and then *verified* to be unconfounded — every arm contributes exactly two samples per
batch, three per passage and three per operator.

**Results.** At n = 6 the design reaches **89% power** for a two-fold change at moderate biological
variability (CV 0.30) and essentially complete power for four-fold changes; the smallest reliably detectable
effect is **1.83-fold**, and the report states plainly that 1.5-fold changes would need 13–39 replicates. The
design predicts, falsifiably, that **HIF1A mRNA falls 20–80% during hypoxia** while HIF-1α protein
accumulates — a result a naive design would misread as experimental failure.

**Deliverable.** A 15-page design report (~4,086 words, 7 tables, 5 figures), a 238-word description, and a
reproducibility bundle. Repository: `genetics-week2-experimental-design`.

---

### Week 3 — Phylogenetic Analysis and Tree Reconstruction

**Task.** Retrieve publicly available genetic sequences, align them, reconstruct a phylogenetic tree, and
interpret it — documenting every step, parameter and assumption.

**Approach.** Cytochrome c oxidase subunit 1 (COX1) across **twelve vertebrate species** spanning jawless
fish, ray-finned fish, amphibian, reptile, two birds and five mammals, including a jawless-fish outgroup.

**Method.** Retrieval from UniProt and NCBI; **reference-identity screening**; multiple sequence alignment
with FAMSA; distance estimation under p-distance, Poisson and BLOSUM62/Kimura models; Neighbour-Joining and
UPGMA reconstruction; and node support from 500 bootstrap replicates.

**Results.** The primate, mammal, bird and ray-finned fish clades were recovered with strong support
(**100%, 94%, 100% and 99%**), and the pairwise divergences matched published values almost exactly:
human–chimpanzee **98.8%** identity, human–mouse **90.8%**, human–chicken **84.6%**, chicken–pigeon **96.3%**.
The deepest nodes were **not resolved by any of seven substitution models**, and the report proves this and
diagnoses the cause — long-branch attraction with sparse taxon sampling, single-gene data, and an anomalously
conserved outgroup record — rather than presenting a misleading tree. It also documents a concrete
data-quality failure: a GenBank record submitted as chicken COX1 was **99.8% identical to human**, which is
why screening is treated as a required analytical step rather than an optional one.

**Deliverable.** A 16-page report (~4,134 words, 5 tables, 8 figures), a 244-word description, and a
43-file reproducibility bundle. Repository: `genetics-week3-phylogenetics`.

---

### Week 4 — Automation of Genetic Data Analysis Pipeline

**Task.** Develop an automated pipeline for processing and analysing genetic data, with annotated code, flow
diagrams and a sample run report demonstrating output and troubleshooting.

**Approach.** I wrote working software rather than describing it: **genePipe**, a Python package of twelve
modules driven by a single validated configuration file and run from the command line, taking a FASTA file
through cleaning, quality control, alignment, variant calling, statistical association testing and
phylogenetic reconstruction in one command.

**Method.** Modular four-layer architecture (entry points → orchestrator → analysis → output, plus shared
utilities); argparse CLI with meaningful exit codes; layered configuration with explicit validation;
structured logging to console and file; a **stage cache** that fingerprints each stage's inputs and
configuration; artefact-based state restoration so a resumed run is correct; SHA-256 provenance capture; and
fail-safe orchestration in which a stage that raises is recorded and the report is still written.

**Results.** **86 automated tests**, all passing. Run on a seeded simulated cohort of 22 sequences, the
pipeline recovered a deliberately planted marker — **g.612C>G, present in 10/10 cases and 0/10 controls**,
the only one of **141 tested sites** to survive Benjamini–Hochberg correction. Run unchanged on real public
COX1 data it reproduced Week 3's groupings (primates 100%, birds 100%, ray-finned fish 99.8%). The stage cache
cut a repeat run from **17.2 seconds to 0.0 seconds**.

**The defect log.** Eleven substantive defects were found and fixed during development, each documented with
its symptom, root cause, fix and regression test. Two are the kind that silently produce wrong science: a
**DNA/protein alphabet collision** (the DNA ambiguity set contains M, S, W, D, H and V, which are valid amino
acids, so protein data was flagged 90% "ambiguous" and would have been masked to death), and a
**saturation-induced crash** in tree building when the Kimura 2-parameter distance became undefined. Others
included a cache that skipped work without restoring state, and an association denominator that counted
samples dropped during cleaning.

**Deliverable.** A 17-page report (~3,949 words, 7 annotated code listings, 4 flow diagrams, 8 figures), a
250-word description, and a 109-file reproducibility bundle. Repository: `genetics-week4-automation-pipeline`.

---

### Week 5 — Critical Review of Genetic Research Methods and Ethical Considerations

**Task.** Conduct a critical review of current genetic research methods while addressing the ethical, legal
and social implications, including case studies, and propose how ethical practice can be integrated into
research workflows.

**Approach.** A ~10,000-word review whose organising claim is that **methodology and ethics are the same
question asked in two vocabularies**: a polygenic score that does not travel across ancestries is both a
scientific defect and a source of health inequity; the irreversibility of germline editing is both a technical
property and the reason it is governed differently from somatic therapy.

**Method.** Targeted literature review giving priority to peer-reviewed primary research, authoritative
instruments (court judgments, regulatory approvals, government guidelines) and contemporaneous reporting for
events where no primary document is public. Quantitative claims are attributed, and where published estimates
differ the range is reported.

**Results.** The review covers the four families of method (reading, associating, editing, predicting) and
compares eleven methods' advantages and limitations; organises ethics around four domains (the individual;
the family and community; society and the state; the human future); analyses **seven documented case
studies** — Henrietta Lacks and HeLa (1951–2023), the Havasupai tribe (1990–2010), Iceland's deCODE database
(1998–2003), He Jiankui's gene-edited twins (2018–2019), forensic genetic genealogy (2018–), the first CRISPR
sickle cell therapies (2023) and India's National Sickle Cell Anaemia Elimination Mission (2023–2025); and
closes with a nine-step framework for integrating ethics into research workflows.

**Deliverable.** A 31-page review (~10,000 words, 10 tables, 7 figures, 64 references), a 279-word
description, a **fact-check ledger** mapping every quantitative claim to its source, and a reproducibility
bundle. Repository: `genetics-week5-elsi-critical-review`.

---

## 3. What the five weeks collectively demonstrate

**Analytical range.** Across the internship I implemented alignment algorithms, variant calling, association
statistics with multiple-testing correction, power analysis, phylogenetic reconstruction under several
substitution models, and bootstrap resampling — each from first principles rather than by calling a
black-box function, which is why each could be explained in the accompanying report.

**Verification as a habit.** Every week produced a result that could be *checked* rather than merely
inspected: a simulated dataset with asserted ground truth (Week 1), a randomisation plan verified to be
unconfounded (Week 2), divergences compared against published values (Week 3), a planted marker recovered
exactly and an 86-test suite (Week 4), and a fact-check ledger (Week 5).

**Honesty about limits.** Four of the five deliverables report, in detail, something that did not work as
hoped — undetectable effect sizes, unresolved deep nodes, eleven defects, contested evidence. In each case the
limitation is quantified and its cause diagnosed rather than acknowledged in passing.

**Reproducibility.** Every week ships a reproducibility bundle containing the scripts, the data or the
retrieval instructions, the intermediate outputs and the report, so that each result can be regenerated
rather than taken on trust.

**Critical and ethical reasoning.** Week 5 shows the same evidence-first discipline applied to questions that
cannot be settled by computation: contested ethical questions are presented with the strongest arguments on
each side, and the review states explicitly where it does not take a position and why.

---

## 4. Repository map

| Week | Canonical repository | Release |
|---|---|---|
| 1 | `genetics-week1-sequence-analysis` | v1.0 |
| 2 | `genetics-week2-experimental-design` | v1.0 |
| 3 | `genetics-week3-phylogenetics` | v1.0 |
| 4 | `genetics-week4-automation-pipeline` | v1.0 |
| 5 | `genetics-week5-elsi-critical-review` | v1.0 |
| — | `genetics-internship-portfolio` (this repository) | v1.0 |

All repositories are under [github.com/rabinarayanpatra350-biotech](https://github.com/rabinarayanpatra350-biotech).
Each per-week repository is the canonical submission for that week and has not been modified since submission;
this portfolio repository exists to index them and to carry the complete set of reports in one place.
