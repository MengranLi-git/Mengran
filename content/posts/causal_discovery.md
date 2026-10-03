---
title: Causal discovery in multivariate extremes
description: "Tail-induced asymmetry enables causal structure learning in high-dimensional multivariate extremes."
date: 2026-04-01
weight: 1
draft: false
toc: false
layout: distill
eyebrow: Research project
hero_subtitle: "Extreme events don't propagate symmetrically. We turn this directional fingerprint into a causal discovery algorithm with formal guarantees, scaling to hundreds of variables and handling latent confounders."
paper_url: https://arxiv.org/abs/2604.21620
paper_pdf: https://arxiv.org/pdf/2604.21620
project_area: Causal discovery
project_summary: "Learning causal graph structure from the directional fingerprints left by multivariate extremes."
project_status: "arXiv preprint; revision in progress following a reject-and-resubmit decision"
project_methods:
- Multivariate extremes
- Tail asymmetry
- Sparse DAG learning
authors:
- Mengran Li
---

<p class="d-lead">
Standard causal discovery breaks down precisely when it matters most — in the tails of a distribution, where rare but high-impact events occur. This project turns that obstacle into a tool. The very features that make extremes hard to model also make them <b>directional</b>.
</p>

## The core idea

When a variable $X$ causally drives $Y$, predicting extreme values of $Y$ from extreme values of $X$ is systematically easier than predicting in the reverse direction. The forward-backward gap in tail prediction risk — we call it <b>tail-induced asymmetry</b> — is non-zero for causal pairs and vanishes for non-causal associations.

{{< rawhtml >}}
<figure class="d-figure">
  <svg viewBox="0 0 720 260" xmlns="http://www.w3.org/2000/svg" role="img" aria-label="Forward vs backward tail prediction risk">
    <defs>
      <marker id="arrowHead" viewBox="0 0 10 10" refX="8" refY="5" markerWidth="7" markerHeight="7" orient="auto">
        <path d="M0,0 L10,5 L0,10 z" fill="var(--d-accent)"/>
      </marker>
      <marker id="arrowHeadGrey" viewBox="0 0 10 10" refX="8" refY="5" markerWidth="7" markerHeight="7" orient="auto">
        <path d="M0,0 L10,5 L0,10 z" fill="var(--d-muted)"/>
      </marker>
    </defs>

    <rect x="20" y="30" width="320" height="210" fill="var(--d-accent-soft)" stroke="var(--d-border)" stroke-width="1" rx="8"/>
    <text x="40" y="60" class="d-svg-muted" style="font-size:11px; letter-spacing:0.08em; text-transform:uppercase; fill:var(--d-accent);">Forward</text>
    <text x="40" y="88" class="d-svg-label" style="font-size:15px; font-weight:600; fill:var(--d-text);">Predict Y from extreme X</text>

    <circle cx="90" cy="160" r="18" fill="var(--d-bg-soft)" stroke="var(--d-accent)" stroke-width="2"/>
    <text x="90" y="165" text-anchor="middle" class="d-svg-label" style="font-weight:600;">X</text>
    <line x1="112" y1="160" x2="228" y2="160" stroke="var(--d-accent)" stroke-width="2.5" marker-end="url(#arrowHead)"/>
    <circle cx="250" cy="160" r="18" fill="var(--d-accent)" stroke="var(--d-accent)" stroke-width="2"/>
    <text x="250" y="165" text-anchor="middle" class="d-svg-label" style="font-weight:600; fill:white;">Y</text>

    <text x="180" y="145" text-anchor="middle" class="d-svg-muted" style="fill:var(--d-accent);">cause</text>
    <text x="180" y="205" text-anchor="middle" class="d-svg-label" style="font-weight:600; fill:var(--d-accent);">Risk → 0</text>

    <rect x="380" y="30" width="320" height="210" fill="var(--d-bg)" stroke="var(--d-border)" stroke-width="1" rx="8"/>
    <text x="400" y="60" class="d-svg-muted" style="font-size:11px; letter-spacing:0.08em; text-transform:uppercase;">Backward</text>
    <text x="400" y="88" class="d-svg-label" style="font-size:15px; font-weight:600;">Predict X from extreme Y</text>

    <circle cx="610" cy="160" r="18" fill="var(--d-bg-soft)" stroke="var(--d-muted)" stroke-width="2"/>
    <text x="610" y="165" text-anchor="middle" class="d-svg-label" style="font-weight:600;">X</text>
    <line x1="588" y1="160" x2="472" y2="160" stroke="var(--d-muted)" stroke-width="2.5" marker-end="url(#arrowHeadGrey)"/>
    <circle cx="450" cy="160" r="18" fill="var(--d-muted)" stroke="var(--d-muted)" stroke-width="2"/>
    <text x="450" y="165" text-anchor="middle" class="d-svg-label" style="font-weight:600; fill:white;">Y</text>

    <text x="530" y="145" text-anchor="middle" class="d-svg-muted">spurious</text>
    <text x="530" y="205" text-anchor="middle" class="d-svg-label" style="font-weight:600;">Risk &gt; 0</text>
  </svg>
  <figcaption class="d-figure-caption">
    <b>Figure 1.</b> Tail-induced asymmetry. When X causes Y, the forward tail prediction risk converges to zero while the backward risk stays bounded away from zero. The gap uniquely identifies causal direction from the joint tail distribution alone.
  </figcaption>
</figure>
{{< /rawhtml >}}

This insight rests on the theory of multivariate regular variation. Under a recursive causal DAG, the angular measure characterising tail dependence encodes directional information consistent with the causal ordering — and that information can be estimated from data.

## Method: S3ME

We propose <b>S3ME</b> — <i>Sparse Structure diScovery in Multivariate Extremes</i> — a two-stage framework designed around the division of labour between <i>which</i> variables connect and <i>how</i> they are oriented.

{{< rawhtml >}}
<figure class="d-figure">
  <svg viewBox="0 0 720 200" xmlns="http://www.w3.org/2000/svg" role="img" aria-label="S3ME two-stage pipeline">
    <defs>
      <marker id="pipeArrow" viewBox="0 0 10 10" refX="8" refY="5" markerWidth="8" markerHeight="8" orient="auto">
        <path d="M0,0 L10,5 L0,10 z" fill="var(--d-muted)"/>
      </marker>
    </defs>

    <rect x="20" y="40" width="140" height="100" rx="8" fill="var(--d-bg-soft)" stroke="var(--d-border)" stroke-width="1.5"/>
    <text x="90" y="70" text-anchor="middle" class="d-svg-muted" style="font-size:10px; letter-spacing:0.08em; text-transform:uppercase;">Input</text>
    <text x="90" y="102" text-anchor="middle" class="d-svg-label" style="font-weight:600;">Heavy-tailed</text>
    <text x="90" y="120" text-anchor="middle" class="d-svg-label" style="font-weight:600;">observations</text>

    <line x1="170" y1="90" x2="210" y2="90" stroke="var(--d-muted)" stroke-width="1.5" marker-end="url(#pipeArrow)"/>

    <rect x="220" y="30" width="180" height="120" rx="8" fill="var(--d-accent-soft)" stroke="var(--d-accent)" stroke-width="1.5"/>
    <text x="310" y="56" text-anchor="middle" class="d-svg-muted" style="font-size:10px; letter-spacing:0.08em; text-transform:uppercase; fill:var(--d-accent);">Stage 1</text>
    <text x="310" y="84" text-anchor="middle" class="d-svg-label" style="font-weight:600;">Skeleton recovery</text>
    <text x="310" y="108" text-anchor="middle" class="d-svg-muted" style="font-size:12px;">Proxy-adjusted</text>
    <text x="310" y="126" text-anchor="middle" class="d-svg-muted" style="font-size:12px;">penalised selection</text>

    <line x1="410" y1="90" x2="450" y2="90" stroke="var(--d-muted)" stroke-width="1.5" marker-end="url(#pipeArrow)"/>

    <rect x="460" y="30" width="180" height="120" rx="8" fill="var(--d-accent-soft)" stroke="var(--d-accent)" stroke-width="1.5"/>
    <text x="550" y="56" text-anchor="middle" class="d-svg-muted" style="font-size:10px; letter-spacing:0.08em; text-transform:uppercase; fill:var(--d-accent);">Stage 2</text>
    <text x="550" y="84" text-anchor="middle" class="d-svg-label" style="font-weight:600;">Edge orientation</text>
    <text x="550" y="108" text-anchor="middle" class="d-svg-muted" style="font-size:12px;">Forward/backward</text>
    <text x="550" y="126" text-anchor="middle" class="d-svg-muted" style="font-size:12px;">tail prediction risk</text>

    <line x1="650" y1="90" x2="690" y2="90" stroke="var(--d-muted)" stroke-width="1.5" marker-end="url(#pipeArrow)"/>

    <text x="700" y="75" class="d-svg-label" style="font-weight:600; fill:var(--d-accent);">DAG</text>
    <text x="700" y="95" class="d-svg-muted" style="font-size:11px;">causal</text>
    <text x="700" y="110" class="d-svg-muted" style="font-size:11px;">graph</text>
  </svg>
  <figcaption class="d-figure-caption">
    <b>Figure 2.</b> S3ME pipeline. Stage 1 recovers which variables connect, using an unpenalised proxy to absorb latent common shocks. Stage 2 orients each edge by comparing the tail prediction risk of the max-linear envelope model in both directions, penalised by EBIC.
  </figcaption>
</figure>
{{< /rawhtml >}}

The two-stage design is deliberate. Skeleton recovery and edge orientation require different tools — penalised regression for one, tail risk minimisation for the other — and separating them lets each stage use the right machinery without compromise.

## Results

### Simulations

S3ME maintains strong edge-recovery performance well beyond the sample size, across a range of dimensions.

{{< rawhtml >}}
<figure class="d-figure">
  <svg viewBox="0 0 720 260" xmlns="http://www.w3.org/2000/svg" role="img" aria-label="F1 score bar chart">
    <line x1="60" y1="220" x2="680" y2="220" stroke="var(--d-muted)" stroke-width="1"/>
    <line x1="60" y1="40" x2="60" y2="220" stroke="var(--d-muted)" stroke-width="1"/>

    <g>
      <text x="54" y="225" text-anchor="end" class="d-svg-muted">0.0</text>
      <line x1="57" y1="220" x2="63" y2="220" stroke="var(--d-muted)"/>
      <text x="54" y="180" text-anchor="end" class="d-svg-muted">0.25</text>
      <line x1="57" y1="175" x2="63" y2="175" stroke="var(--d-muted)"/>
      <line x1="60" y1="175" x2="680" y2="175" stroke="var(--d-border)" stroke-dasharray="3,3"/>
      <text x="54" y="135" text-anchor="end" class="d-svg-muted">0.50</text>
      <line x1="57" y1="130" x2="63" y2="130" stroke="var(--d-muted)"/>
      <line x1="60" y1="130" x2="680" y2="130" stroke="var(--d-border)" stroke-dasharray="3,3"/>
      <text x="54" y="90" text-anchor="end" class="d-svg-muted">0.75</text>
      <line x1="57" y1="85" x2="63" y2="85" stroke="var(--d-muted)"/>
      <line x1="60" y1="85" x2="680" y2="85" stroke="var(--d-border)" stroke-dasharray="3,3"/>
      <text x="54" y="45" text-anchor="end" class="d-svg-muted">1.00</text>
      <line x1="57" y1="40" x2="63" y2="40" stroke="var(--d-muted)"/>
    </g>

    <text x="30" y="130" text-anchor="middle" class="d-svg-muted" transform="rotate(-90 30 130)">F1 score</text>

    <g>
      <rect x="120" y="69.6" width="90" height="150.4" fill="var(--d-accent)" rx="3"/>
      <text x="165" y="62" text-anchor="middle" class="d-svg-label" style="font-weight:600;">0.84</text>
      <text x="165" y="240" text-anchor="middle" class="d-svg-label">p = 20</text>

      <rect x="240" y="80.8" width="90" height="139.2" fill="var(--d-accent)" opacity="0.85" rx="3"/>
      <text x="285" y="73" text-anchor="middle" class="d-svg-label" style="font-weight:600;">0.79</text>
      <text x="285" y="240" text-anchor="middle" class="d-svg-label">p = 50</text>

      <rect x="360" y="84.4" width="90" height="135.6" fill="var(--d-accent)" opacity="0.7" rx="3"/>
      <text x="405" y="76" text-anchor="middle" class="d-svg-label" style="font-weight:600;">0.77</text>
      <text x="405" y="240" text-anchor="middle" class="d-svg-label">p = 100</text>

      <rect x="480" y="98.8" width="90" height="121.2" fill="var(--d-accent)" opacity="0.55" rx="3"/>
      <text x="525" y="91" text-anchor="middle" class="d-svg-label" style="font-weight:600;">0.71</text>
      <text x="525" y="240" text-anchor="middle" class="d-svg-label">p = 200</text>
    </g>

    <text x="640" y="60" class="d-svg-muted" style="font-size:11px;">n = 1,000</text>
    <text x="640" y="76" class="d-svg-muted" style="font-size:11px;">50 reps</text>
  </svg>
  <figcaption class="d-figure-caption">
    <b>Figure 3.</b> F1 scores for S3ME across increasing dimensionality. Performance holds up as the number of variables grows well beyond the sample size, a regime where classical causal discovery methods struggle without strong parametric assumptions.
  </figcaption>
</figure>
{{< /rawhtml >}}

The method is robust to moderate misspecification of the tail model and to moderate levels of latent confounding.

### Real data

<div class="d-cards">
  <div class="d-card">
    <div class="d-card-tag">Hydrology</div>
    <h4>Danube River Network</h4>
    <p>Applied to daily flow maxima at 31 gauging stations across the Danube basin. The recovered causal graph correctly reflects upstream-to-downstream flow direction at the majority of station pairs, using no geographic or hydrological prior information.</p>
  </div>
  <div class="d-card">
    <div class="d-card-tag">Finance</div>
    <h4>S&amp;P 500 Tail Risk</h4>
    <p>Applied to weekly minimum returns for 103 stocks over a 20-year period. The method identifies directional tail risk propagation across sectors, recovering known contagion pathways during historical market stress periods.</p>
  </div>
</div>

## Broader significance

This work re-frames tail behaviour from nuisance to signal. Wherever extreme events propagate through a system with underlying causal structure, tail asymmetry provides a tool to recover that structure — even in regimes where classical causal discovery methods have no leverage.

<div class="d-cta">
  <h3 style="margin-top:0;">Read the paper</h3>
  <p style="margin-bottom:0;">Full theoretical development, proofs, simulation design, and the Danube and S&amp;P 500 case studies are available in the arXiv preprint.</p>
  <div class="d-cta-buttons">
    <a class="d-btn d-btn-primary" href="https://arxiv.org/abs/2604.21620" target="_blank" rel="noopener">arXiv:2604.21620</a>
    <a class="d-btn d-btn-ghost" href="https://arxiv.org/pdf/2604.21620" target="_blank" rel="noopener">PDF</a>
  </div>
</div>
