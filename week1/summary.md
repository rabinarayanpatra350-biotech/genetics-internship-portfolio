# Week 1 — Genetic Sequence Analysis and Reporting

**Status:** submitted and graded | **Repository:** [genetics-week1-sequence-analysis](https://github.com/rabinarayanpatra350-biotech/genetics-week1-sequence-analysis) | **Release:** v1.0

## The task

Conduct a bioinformatics analysis of genetic sequence data: design or obtain a dataset, analyse it, and report
the findings with full documentation of methods, results and limitations.

## What was produced

A **14-page report** (~3,828 words, 6 tables, 8 figures, 12 references), a 232-word portal description, and a
55-file reproducibility bundle. The report includes annotated screenshots of the analysis process.

## Approach

Rather than analyse an arbitrary public sequence, I designed a **self-verifying simulated dataset** so the
analysis could be checked against known ground truth.

- **SIMG1**, a 1,500 bp simulated gene: 5' UTR, a 1,299 bp coding sequence carrying a glycine-rich loop and a
  catalytic DxxxxN motif, and a 3' UTR with a polyadenylation signal
- **Twelve samples** (six cases, six controls) with a documented catalogue of substitutions, in-frame
  deletions, two premature-stop variants and a frameshift, all from a fixed random seed
- The simulation script **asserts every designed effect** after construction, so the dataset verifies itself

## Methods (six documented steps)

1. Quality control and six-frame ORF detection
2. Global Needleman–Wunsch alignment with exact variant calling and functional annotation
3. BLAST-style seed-and-extend homology search against a four-sequence database
4. Multiple sequence alignment with conservation profiling and an enrichment test
5. Substitution-spectrum analysis
6. Fisher exact association testing with Bonferroni correction

Implemented in Python with Biopython, FAMSA and SciPy.

## Key results

| Result | Value |
|---|---|
| Variant calls | **81 calls at 13 sites** (74 SNVs, 6 deletions, 1 insertion) |
| Transition / transversion ratio | **2.36** |
| Conserved alignment positions | 830 of 1,500 |
| Candidate marker | **g.612C>G (P171R)** — 6/6 cases, 0/6 controls, Fisher **p = 0.0022**, survives Bonferroni |
| Loss-of-function variants | 3, truncating the protein to 39, 42 and 404 residues |
| Homology search | self 100% / 1,500 bp / E = 0; homolog 88.21% / 1,493 bp; distant 65.27% / 239 bp / E = 7.32e-12 |

## What it demonstrates

Sequence-level analysis implemented from first principles, a ground-truth-checkable dataset design, and
statistical rigour in the association testing (exact test plus multiple-testing correction rather than a
nominal p-value).
