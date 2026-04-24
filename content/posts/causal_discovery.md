---
title: Causal discovery in multivariate extremes
description: "Tail-induced asymmetry enables causal structure learning in high-dimensional multivariate extremes. We develop methods that exploit directional information encoded by tail dependence patterns to recover causal graphs in extreme regimes."
date: 2026-04-01
weight: 1
draft: false
toc: true
authors:
- Mengran Li
---

## Project Overview

Causal discovery — the problem of inferring causal structure from observational data — is central to modern machine learning and scientific inquiry. However, most existing methods rely on assumptions that break down in extreme regimes. Standard approaches assume approximate linearity, additivity, or at least well-behaved distributions — none of which hold for rare, high-impact events where causal understanding is most consequential.

This project develops a fundamentally different approach: instead of fighting the complexity of extreme behaviour, we **exploit it**. Our key insight is that in multivariate extremes, the tail itself contains directional information that can reveal causal structure. When one variable causally influences another, predicting extreme values forward (cause to effect) is fundamentally easier than predicting backward — a signature that vanishes for non-causal relationships.

By characterising and measuring this tail-induced asymmetry, we recover causal directed acyclic graphs (DAGs) in settings where traditional methods fail, including high-dimensional settings with latent confounders.

### Goals

1. **Theoretical Foundation**: Establish conditions under which tail asymmetry identifies causal direction in multivariate extremes.

2. **Methodological Innovation**: Develop practical algorithms combining extreme value statistics with causal discovery, handling latent confounders and $p \gg n$ settings.

3. **Empirical Validation**: Demonstrate the approach on real-world network data from hydrology and finance.

---

## Methodology: S3ME

We propose **S3ME** (*Sparse Structure diScovery in Multivariate Extremes*), a two-stage framework:

| Component | Challenge | S3ME Solution |
|:----------|:----------|:--------------|
| **Skeleton Recovery** | Latent confounders create spurious tail associations | Proxy-adjusted penalised neighbourhood selection absorbs common shocks |
| **Edge Orientation** | Causal direction is unidentifiable without tail structure | Compare forward vs. backward tail prediction risk using max-linear envelope models |
| **High Dimensions** | DAG learning scales poorly with $p$ | EBIC penalty enforces sparsity; sure screening guarantees no true edge is missed |

**Core Innovation**: The tail prediction risk asymmetry is non-zero for causal pairs and negligible for non-causal ones, providing a consistent and estimable causal signal directly from extremes.

---

## Key Findings

### Simulation Study

We evaluate S3ME across dimensions $p = 20, 50, 100, 200$ with $n = 1{,}000$ observations and 50 replicates per setting:

| Dimension | F1 Score |
|:---:|:---:|
| $p = 20$ | 0.837 |
| $p = 50$ | 0.790 |
| $p = 100$ | 0.770 |
| $p = 200$ | 0.710 |

- **Robustness**: Performance holds under moderate misspecification of the tail model and in the presence of latent confounding.
- **Scaling**: S3ME successfully recovers the DAG skeleton in $p \gg n$ settings where standard methods require strong parametric assumptions.

### Real Data Applications

**Danube River Network**: We apply S3ME to daily flow maxima at 31 gauging stations across the Danube basin. The recovered causal graph aligns with known upstream-to-downstream flow relationships, correctly orienting the majority of edges without using any geographic prior information.

**S&P 500 Tail Risk**: Applied to weekly minimum returns for 103 stocks over a 20-year period, S3ME identifies directional tail risk propagation across sectors, recovering known contagion pathways during historical market stress periods.

---

## Impact & Outputs

📄 **arXiv Preprint**  
*Causal Discovery in Multivariate Extremes via Tail Asymmetry*  
[arXiv:2604.21620](https://arxiv.org/abs/2604.21620) | [PDF](https://arxiv.org/pdf/2604.21620)

🎯 **Broader Significance**  
This framework establishes a new paradigm for causal discovery by treating tail asymmetry as a source of causal information rather than a nuisance, with applications across:
- **Hydrology**: Causal structure in river networks and flood propagation
- **Finance**: Directional tail risk and systemic contagion mapping
- **Environmental science**: Extreme event propagation across monitoring networks

---

**Status:** arXiv preprint (April 2026)

**Paper:** [Causal Discovery in Multivariate Extremes via Tail Asymmetry](https://arxiv.org/abs/2604.21620)
