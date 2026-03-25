---
title: Extreme quantile treatment effect (EQTE)
description: "Extreme quantile treatment effects (eQTEs) measure causal impacts on outcome distribution tails. We propose the TIEE framework combining information across quantile levels with extreme value models, enabling causal inference for rare, high-impact events in environmental risk, economics, and public health."
date: 2025-10-01
weight: 2
draft: false
toc: true
---

## Project Overview

Extreme quantile treatment effects (eQTEs) measure the causal impact of a treatment on the tails of an outcome distribution. Unlike average treatment effects, eQTEs capture how interventions affect rare, high-impact outcomes—critical for understanding climate extremes, financial crashes, or public health crises where the tail behavior matters most.

Standard QTE methods struggle in extreme regimes due to data sparsity: by definition, extreme quantiles lie beyond observed data. Existing eQTE approaches rely on restrictive tail assumptions or apply interior-quantile theory that may not extend to the far tail. This creates a fundamental tension between the causal question (what is the treatment effect at extreme levels?) and the statistical challenge (how to estimate beyond observed data?).

This project develops the **Tail-Calibrated Inverse Estimating Equation (TIEE)** framework, which bridges this gap by combining information across quantile levels while anchoring the tail using extreme value theory.

### Goals

1. **Unified Framework**: Develop an estimating equation approach that integrates interior quantile information with tail extrapolation in a principled manner.

2. **Robust Inference**: Establish asymptotic properties and valid uncertainty quantification for extreme causal effects.

3. **Practical Impact**: Enable causal attribution for rare events in environmental science, economics, and public health.

---

## Methodology: The TIEE Framework

The TIEE framework addresses the core challenge of extreme causal inference through three key innovations:

| Component | Challenge | TIEE Solution |
|:----------|:----------|:--------------|
| **Tail Anchoring** | Extreme quantiles lack direct data | Use Extreme Value Theory (EVT) models for tail extrapolation |
| **Information Borrowing** | Interior and tail estimates are disconnected | Unified estimating equation across all quantile levels |
| **Causal Identification** | Treatment effects at extremes require careful handling | Inverse probability weighting adapted for tail regimes |

**Core Innovation**: The TIEE estimator combines:
- **Inverse estimating equations** for causal identification
- **Tail calibration** using generalized Pareto distributions
- **Cross-quantile information** to stabilize extreme estimates

This allows valid inference at quantile levels where traditional methods fail, while properly propagating uncertainty from both the causal and extreme value components.

---

## Key Findings

### Simulation Study

Our simulations evaluated TIEE under different tail behaviours (light, exponential, heavy) and model misspecifications:

- **Performance**: TIEE maintains valid coverage and low bias even at extreme quantiles (e.g., 0.99, 0.995) where standard QTE methods break down.
- **Robustness**: The framework shows resilience to moderate misspecification of the tail model, thanks to information borrowing across quantile levels.
- **Efficiency**: Leveraging interior quantile data improves precision compared to pure EVT extrapolation.

### Real Data Application: Austrian Alps Precipitation

We applied TIEE to study the causal effect of anthropogenic warming on extreme precipitation in the Austrian Alps:

- **Causal Question**: How has climate change altered the probability of extremely high precipitation events?
- **Methodological Contribution**: TIEE enables observational causal attribution for rare events under a counterfactual framework.
- **Scientific Insight**: The framework reveals how treatment effects vary across the outcome distribution—not just at the mean, but at the extremes where climate impacts are most consequential.

---

## Impact & Outputs

📄 **arXiv Preprint**  
*Tail-Calibrated Estimation of Extreme Quantile Treatment Effects*  
[arXiv:2603.23309](https://arxiv.org/abs/2603.23309) | [PDF](https://arxiv.org/pdf/2603.23309)

🎯 **Broader Significance**  
This framework establishes a new foundation for causal inference on rare, high-impact outcomes, with applications across:
- **Environmental risk**: Climate extreme attribution
- **Economics**: Tail risk in financial markets
- **Public health**: Rare disease treatment effects

---

**Status:** arXiv preprint (March 2026)

**Paper:** [Tail-Calibrated Estimation of Extreme Quantile Treatment Effects](https://arxiv.org/abs/2603.23309)
