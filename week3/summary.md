# Week 3 — Phylogenetic Analysis and Tree Reconstruction

**Status:** submitted and graded | **Repository:** [genetics-week3-phylogenetics](https://github.com/rabinarayanpatra350-biotech/genetics-week3-phylogenetics) | **Release:** v1.0

## The task

Retrieve publicly available genetic sequences, align them, reconstruct a phylogenetic tree, and interpret it —
documenting alignment methods, tree construction parameters and every assumption made.

## What was produced

A **16-page report** (~4,134 words, 5 tables, 8 figures, 24 references), a 244-word portal description, and a
43-file reproducibility bundle containing the retrieved sequences, the alignment, all distance matrices and
the tree files.

## Dataset

Cytochrome c oxidase subunit 1 (**COX1 / MT-CO1**) across **twelve vertebrate species** spanning jawless fish,
ray-finned fish, amphibian, reptile, two birds and five mammals, with the jawless fish as outgroup. Retrieved
from UniProt (curated entries) and NCBI (nucleotide barcodes).

## Methods

Sequence retrieval → **reference-identity screening** → multiple sequence alignment (FAMSA) → distance
estimation under p-distance, Poisson and BLOSUM62/Kimura models → Neighbour-Joining and UPGMA reconstruction →
node support from **500 bootstrap replicates** → saturation and molecular-clock diagnostics.

## Key results

| Clade | Bootstrap support |
|---|---|
| *Homo sapiens* + *Pan troglodytes* | **100%** |
| Mammals (5 species) | **94%** |
| *Gallus gallus* + *Columba livia* | **100%** |
| *Danio rerio* + *Salmo salar* | **99%** |

| Pair | Observed identity | Published expectation |
|---|---|---|
| human – chimpanzee | **98.8%** | ~99% |
| human – mouse | **90.8%** | ~90% |
| human – chicken | **84.6%** | ~84% |
| chicken – pigeon | **96.3%** | ~96% |

## Two findings reported rather than hidden

1. **The deepest nodes are not resolved** by any of seven substitution models. The report *proves* this
   (all models fail identically, bootstrap 14% at the reptile node) and diagnoses the cause — long-branch
   attraction with sparse taxon sampling, single-gene data, and an anomalously conserved outgroup record —
   rather than drawing a tree the evidence does not support.
2. **A data-quality failure in a public record.** A GenBank entry submitted as chicken COX1 was **99.8%
   identical to human** — impossible for a bird. Screening every record against a reference before alignment
   is therefore treated as a required step, not an optional one.

## What it demonstrates

Real public-data retrieval and screening, distance-based phylogenetics under multiple substitution models,
bootstrap support estimation, and the discipline to report an unresolved result as unresolved — with eight
concrete recommendations for future studies.
