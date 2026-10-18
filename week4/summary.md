# Week 4 — Automation of Genetic Data Analysis Pipeline

**Status:** submitted and graded | **Repository:** [genetics-week4-automation-pipeline](https://github.com/rabinarayanpatra350-biotech/genetics-week4-automation-pipeline) | **Release:** v1.0

## The task

Develop an automated pipeline for processing and analysing genetic data, documented with annotated code, flow
diagrams, and a sample run report demonstrating output and troubleshooting steps.

## What was produced

Working software — **genePipe** — plus a **17-page report** (~3,949 words, 7 annotated code listings, 4 flow
diagrams, 8 figures), a 250-word portal description, and a 109-file reproducibility bundle.

## The software

A Python package of **twelve modules** in four layers (entry points → orchestrator → analysis → output, plus
shared utilities), driven by a single validated configuration file and run from the command line:

```bash
python3 -m genepipe run --input data/sample.fasta --out results/run1 --groups data/groups.json
```

One command takes a FASTA file through **cleaning → quality control → alignment → variant calling →
statistical association testing → phylogenetic reconstruction** and writes a documented run report.

## Engineering features

- **86 automated tests** (pytest), one file per module, including end-to-end and caching tests
- **Stage cache** — fingerprints each stage's inputs and configuration; a repeat run drops from **17.2 s to
  0.0 s**
- **Artefact-based state restoration** so a resumed run is correct, not just fast
- **Fail-safe orchestration** — a stage that raises is recorded, independent stages still run, the report is
  always written
- **No third-party dependencies in the core** — runs on a bare Python 3.10+ interpreter
- **Provenance** — version, interpreter, platform, SHA-256 input fingerprint and a configuration snapshot per
  run

## Key results

| Run | Result |
|---|---|
| Seeded simulated cohort (22 sequences) | Planted marker **g.612C>G** recovered exactly — **10/10 cases, 0/10 controls**, the only one of **141 tested sites** to survive Benjamini–Hochberg correction (adjusted p = 0.0015) |
| Real public COX1 data (12 vertebrates) | Reproduced Week 3's groupings: primates **100%**, birds **100%**, ray-finned fish **99.8%** bootstrap |
| Efficiency | Repeat run **17.2 s → 0.0 s** via the stage cache |

## The defect log — eleven defects found and fixed

Each is documented with its symptom, root cause, fix and the regression test that now guards it. Two would
have silently produced wrong science:

- **A DNA/protein alphabet collision** — the DNA ambiguity set contains M, S, W, D, H and V, which are valid
  amino acids; protein data was flagged 90% "ambiguous" and would have been masked to death
- **A saturation-induced crash** — the Kimura 2-parameter distance is undefined at saturation, and the
  resulting NaN broke tree building until a documented p-distance fallback was added

Others included a cache that skipped computation without restoring state, an association denominator that
counted samples dropped during cleaning, and a "report" stage that was listed as runnable but had no handler.

## What it demonstrates

Software engineering applied to genetics: package design, CLI ergonomics, layered configuration, logging,
caching, provenance, a real test suite, and — most importantly — an honest account of how the software failed
before it worked.
