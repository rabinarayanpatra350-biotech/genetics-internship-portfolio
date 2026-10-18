# Week 2 — Experimental Design Simulation for Gene Expression Analysis

**Status:** submitted and graded | **Repository:** [genetics-week2-experimental-design](https://github.com/rabinarayanpatra350-biotech/genetics-week2-experimental-design) | **Release:** v1.0

## The task

Design an experiment for gene expression analysis: choose and justify the methodology, set out the full
procedure, state expected results, and provide a troubleshooting and validation plan.

## What was produced

A **15-page design report** (~4,086 words, 7 tables, 5 figures, 20 references) and a 238-word portal
description, plus a reproducibility bundle containing the computed power analysis and randomisation plan.

## The designed experiment

A controlled **RNA-seq study of hypoxia and reoxygenation injury in human endothelial cells**, with orthogonal
qRT-PCR validation.

| Arm | Condition | Purpose |
|---|---|---|
| A | Normoxia, control siRNA | Baseline control |
| B | Hypoxia 1% O₂, 24 h | Hypoxia effect |
| C | Hypoxia → reoxygenation | Reperfusion effect |
| D | Hypoxia + HIF1A siRNA | Mechanism arm |

Four arms × six biological replicates = 24 libraries, balanced across three processing batches, two cell
passages and two operators.

## The design decisions were computed, not asserted

- **Sample size** from a negative-binomial power analysis (Hart et al. 2013), implemented in the accompanying
  code
- **Randomisation plan** generated programmatically and then *verified* to be unconfounded — every arm
  contributes exactly two samples per batch, three per passage, three per operator
- **Four categories of control** and an explicit variable structure separating controlled from confounding
  factors

## Key results

| Result | Value |
|---|---|
| Power at n = 6, 2-fold change, CV 0.30 | **89%** |
| Power at n = 6, 4-fold change | essentially complete |
| Smallest reliably detectable effect at n = 6 | **1.83-fold** |
| Honest limit stated | 1.5-fold changes would need 13–39 replicates |
| Falsifiable prediction | **HIF1A mRNA falls 20–80% during hypoxia** while HIF-1α protein accumulates |

## What it demonstrates

Quantitative experimental design — power analysis, verified randomisation, pre-specified contrasts and
falsifiable predictions with numbers — plus the willingness to state what the design *cannot* detect. The
counter-intuitive HIF1A prediction is included deliberately because a design that does not expect it would
misread a successful experiment as a failure.
