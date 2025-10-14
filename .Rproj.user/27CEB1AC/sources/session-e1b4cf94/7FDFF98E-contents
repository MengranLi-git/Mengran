---
title: Extreme Event Attribution (EEA)
description: Exploring how tail assumptions influence attribution of extreme climate events, combining simulation, spatial methodology, and software development.
date: 2025-07-01
weight: 2
draft: false
toc: true
authors:
- Mengran Li
---

## Project Overview

Extreme Event Attribution (EEA) is a vital field that assesses the extent to which human-induced climate change influences the probability and intensity of specific extreme weather events. As these events are becoming more frequent and intense, the need for robust statistical tools to underpin these assessments is more critical than ever.

Attribution studies often rely on complex statistical models to characterize the behavior of rare events residing in the tail of the climate data distribution. The challenge is that climate extremes are inherently multivariate and high-dimensional. Therefore, the model choice is critical, as it must accurately capture the joint tail behaviour—the way these extreme variables occur together. Errors in modeling this tail dependence can lead to significant biases in attributing climate change's influence.

This project employs a counterfactual causal inference framework, comparing the factual world (with human influence) against a counterfactual world (without human influence). Within this framework, we compare three distinct multivariate models designed to handle high-dimensional extreme data. Our objective is to estimate Attribution Ratios (ARs), which quantify the probability that human influence was necessary for the event's occurrence.

### Goals

1. Sensitivity Analysis: We aim to show precisely how the choice of tail model in EEA affects the resulting causal attribution conclusion.

2. Practical Guidance: We will offer concrete, practical guidance for selecting and validating appropriate tail models in this context, thereby enhancing the scientific rigor and reliability of future attribution studies.

---

## Methodology: Comparing Three Multivariate Tail Models

We employ a counterfactual causal inference framework, comparing three advanced multivariate models that represent different theoretical assumptions about extremal dependence.

| Model | Core Concept & Assumption | Key Feature |
| :--- | :--- | :--- |
| **Multivariate GPD (mGPD)** | A peaks-over-threshold model built on an exponential random vector. | Assumes a **rigid dependence structure** (limited flexibility in how variables co-occur). |
| **Exponential Factor Copula (eFCM)** | Uses a shared exponential factor ($V$) added to a Gaussian process to induce spatial dependence. | Provides **flexible dependence via mixing**, well-suited for regional extremes that decay with distance. |
| **Huser-Wadsworth (HW) Model** | A multiplicative model that bridges two theoretical regimes (asymptotic independence and dependence). | A **unified, data-driven model** where parameter $\delta$ lets the data decide the strength of the tail link. |

**Key Research Focus:** We measure the models' performance by estimating conditional dependence $\mathbb{P}(U_2 > u \mid U_1 > u)$ as $u \to 1$ and observing how significant model discrepancies (misspecification) propagate to the final AR estimates.

## Core Findings from Simulation & Application

### A. Simulation Study: Impact of Model Misspecification

* **Critical Result:** Simulation Study 1 confirmed that misspecification of the **extremal dependence structure** leads to **substantial bias** in probability estimates ($\hat{p}$). Accurate marginal distributions alone are insufficient.
* **Performance:** Study 2 showed that the **eFCM consistently outperforms the mGPD** in recovering the true tail probability, especially as the true underlying dependence strength increases. This validates the need for flexibility.

### B. Real Data Application: Multi-Region Attribution

We applied the models to two distinct climate datasets: **European winter precipitation maxima** (CNRM model) and **U.S. daily precipitation** (ACCESS-CM2 model).

* **Model Fit:** The **eFCM** provided the best empirical fit for tail dependence in both regions, while the mGPD consistently showed overly strong, rigid dependence.
* **Impact on ARs:** The model choice strongly influences the spatial pattern of attribution:
    * **Rigid Tails (mGPD):** Produced overly smooth maps and consistently **overstated Attribution Ratios (ARs)** across broad regions.
    * **Flexible Tails (eFCM/HW):** Revealed **realistic, regionally varying AR patterns**, aligning better with physical and regional climate insights.

**Application Conclusion:** Rigid tail assumptions severely bias attribution results. Flexible models are essential to reveal the true regional contrasts in the influence of climate change.


## Conclusions and Guidance

### Key Conclusions

* **Tail Dependence Matters:** Attribution results depend critically on how joint extremes are modeled; **misspecifying the tail structure can bias or reverse conclusions.**
* **Model Flexibility Improves Credibility:** **eFCM/HW** fit tails well; **mGPD** overstates ARs. Choosing the right extremal dependence model is **essential for credible EEA.**

### Practical Guidance for Future EEA Studies

| Tip | Rationale |
| :--- | :--- |
| **Prioritise Dependence Structure.** | Simulation results show dependence error is the dominant source of bias in probability estimation. |
| **Do Not Trust Margins Alone.** | Good marginal fit does not guarantee a realistic tail dependence structure. |
| **Prefer Robust Models.** | Choose models with built-in flexibility (like eFCM or HW) that yield more stable AR estimates and narrower uncertainty intervals. |
| **Choose Interpretability.** | Select models that produce scientifically defensible and usable AR patterns. |

## Impact & Recognition

This project has led to significant outputs and recognition within the statistical and climate communities.

* 📄 **Journal Article** A manuscript, *"On the importance of tail assumptions in climate extreme event attribution"*, is currently **under review**.
    [arXiv:2507.14019](https://arxiv.org/abs/2507.14019)
* 🧰 **Software Release** Developed and released the **eFCM R package on CRAN**.
* 🏆 **Major Award:** Received the **3rd Place Award** in the IASC Data Analysis Competition, resulting in an invited talk and award ceremony at the **ISI World Statistics Congress 2025**.
* 🏅 **Presentations:** Talks (WSC 2025 - Travel grant awarded, STOR-i Extremes Workshop, RSC 2023 - Travel grant recipient) and poster (RSS 2025).


