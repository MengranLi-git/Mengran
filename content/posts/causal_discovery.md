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

Causal discovery—the problem of inferring causal structure from observational data—is central to modern machine learning and scientific inquiry. However, most existing methods rely on assumptions that break down in extreme regimes. Standard approaches assume approximate linearity, additivity, or at least well-behaved distributions—none of which hold for rare, high-impact events where we may need causal insights the most.

This project develops a fundamentally different approach: instead of fighting the complexity of extreme behavior, we **exploit it**. Our key insight is that in multivariate extremes, the tail itself contains directional information that can reveal causal structure. When one variable causally influences another, their joint tail behavior exhibits **asymmetry**—a signature that disappears for independent or purely associative relationships.

By characterizing and measuring this tail-induced asymmetry, we can recover causal directed acyclic graphs (DAGs) in settings where traditional methods fail. This enables structure learning for high-dimensional extremes with formal identifiability guarantees.

### Goals

1. **Theoretical Foundation**: Establish conditions under which tail asymmetry identifies causal direction in multivariate extremes.

2. **Methodological Innovation**: Develop practical algorithms that combine extreme value statistics with causal discovery techniques.

3. **High-Dimensional Scaling**: Enable structure learning in settings where the number of variables exceeds sample size—a common challenge in climate and environmental data.

---

## Methodology: Tail-Induced Asymmetry

Our approach leverages a fundamental property of extreme causal relationships: the tail encodes direction.

| Component | Standard Challenge | Tail Asymmetry Solution |
|:----------|:-------------------|:------------------------|
| **Directionality** | Conditional independence tests struggle to distinguish $X \to Y$ from $Y \to X$ | Tail conditional distributions $\mathbb{P}(Y > y \mid X > x)$ become asymmetric as $x, y \to \infty$ for directed pairs |
| **Confounding** | Latent confounders create spurious associations | Extreme regions can reveal the underlying causal skeleton even with hidden confounding |
| **High Dimensionality** | DAG learning scales poorly with $p$ | Tail-based methods naturally prune impossible edges using extremal dependence patterns |

**Core Innovation**: We define and estimate a tail asymmetry measure that:
- Is zero for non-causal relationships (independent or bidirectional association)
- Is non-zero and directionally informative for causal relationships
- Can be estimated consistently from finite samples using extreme value theory
- Scales to high dimensions through conditional independence testing in the tail

The theoretical foundation rests on the extremal representation of multivariate distributions and the observation that the angular measure characterizing tail dependence contains directional information that aligns with causal structure.

---

## Key Findings

### Theoretical Results

We establish formal identifiability guarantees for causal discovery via tail asymmetry:

- **Identifiability**: Under mild assumptions on the causal mechanism, the sign of tail asymmetry uniquely identifies causal direction in a pair of variables.

- **Markov Property in the Tail**: Causal Markov properties extend to extremal dependence, enabling DAG skeleton recovery using tail-based conditional independence tests.

- **Latent Confounding**: Our framework extends to settings with latent confounders, where tail behavior can still reveal the causal skeleton.

### Simulation Study

We evaluated our approach across various data-generating mechanisms and dimensions:

- **Accuracy**: Tail asymmetry correctly identifies causal direction in over 95% of directed pairs across linear and nonlinear mechanisms, even with moderate sample sizes.

- **Robustness**: The method maintains performance under misspecification of the tail model and in the presence of moderate latent confounding.

- **High-Dimensional Scaling**: In settings with $p > n$, our conditional independence tests successfully recover the true DAG skeleton, outperforming standard methods that fail without strong parametric assumptions.

### Real Data Application

We applied our framework to multivariate climate extremes, where causal structure informs understanding of extreme event propagation:

- **Climate Networks**: The recovered causal graph aligns with known atmospheric circulation patterns, revealing directional influence between regional extreme precipitation events.

- **Event Attribution**: The structure enables targeted causal attribution by isolating the relevant causal pathways for specific extreme events.

---

## Impact & Outputs

📄 **arXiv Preprint**  
*Causal Discovery in Multivariate Extremes via Tail Asymmetry*  
[arXiv:2604.21620](https://arxiv.org/abs/2604.21620) | [PDF](https://arxiv.org/pdf/2604.21620)

🎯 **Broader Significance**  
This work establishes a new paradigm for causal discovery by treating tail behavior not as a nuisance, but as a source of causal information. Applications include:
- **Climate science**: Understanding causal structure in extreme weather patterns
- **Finance**: Identifying directional tail risk propagation
- **Systems biology**: Reconstructing causal networks from extreme response data

---

**Status:** arXiv preprint (April 2026) | Under review at *JASA* (Theory & Methods)

**Paper:** [Causal Discovery in Multivariate Extremes via Tail Asymmetry](https://arxiv.org/abs/2604.21620)
