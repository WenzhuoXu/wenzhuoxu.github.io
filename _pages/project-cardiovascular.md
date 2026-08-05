---
title: "Super-resolution for cardiovascular blood flow"
permalink: /projects/cardiovascular-super-resolution/
layout: single
classes: wide
author_profile: false
read_time: false
share: false
---

BioSiMMlab & Design Research Collective, Carnegie Mellon University · 2025 · presented at APS-DFD 2025, Houston
{: .project-meta}

<div class="project-hero" markdown="0">
<img src="/assets/projects/cardiovascular-super-resolution/hero.webp" alt="Three renders of the same diseased coronary artery tree coloured by time-averaged wall shear stress. The low-resolution input is almost uniformly dark blue; the ML prediction and the high-resolution CFD reference both show matching green and orange high-shear bands near the stenosis and the bifurcations.">
</div>

Wall shear stress is the number a cardiologist wants out of a coronary flow simulation. It is the force blood drags along the artery wall, and where it goes abnormal is where plaque is likely to be dangerous. It is also the single quantity a coarse mesh is worst at, because it is a gradient measured right at the wall — exactly where a cheap mesh has the fewest points.

So you are stuck. The simulation that gives you a trustworthy answer takes twelve hours per patient. The one that finishes over lunch tells you the wall is nearly quiescent when it is not. Look at the left panel above: that is the same artery, same blood, same heartbeat as the right panel. The coarse run just cannot see the shear.

<div class="stat-strip" markdown="0">
  <span class="stat"><span class="stat__value">35×</span><span class="stat__label">faster than high-fidelity CFD</span></span>
  <span class="stat"><span class="stat__value">87.7k → 3.05M</span><span class="stat__label">elements, coarse input to target mesh</span></span>
  <span class="stat"><span class="stat__value">0.92–0.94</span><span class="stat__label">WSS correlation against the reference solver</span></span>
  <span class="stat"><span class="stat__value">20.3 min</span><span class="stat__label">end to end, against 12 hours</span></span>
</div>

## Decompose, then correct

A neural network that has to look at a three-million-element artery all at once is a network that will run out of memory before it runs out of patience. The fix is to stop asking it to. The mesh is cut into overlapping subdomains, each small enough to reason about locally, and each is corrected independently. The overlap is the load-bearing part: it is what keeps the reconstruction continuous when the pieces are stitched back together, so you do not get seams where two subdomains disagree.

{% include figure.html src="/assets/projects/cardiovascular-super-resolution/decomposition.webp" alt="Close-up of a wireframe vessel mesh with two overlapping quadrilateral patches shaded purple and orange, labelled subdomain 0, overlap, and subdomain 1." caption="Two subdomains and the band they share. Each patch is solved on its own; the overlap is what makes the seam invisible." %}

Training used 18 of the 24 synthetic left-coronary geometries — 12 healthy and 6 diseased, giving 193,536 subdomain samples — with 6 diseased geometries held out for testing. The geometries come from a parametric model of the left coronary tree, varying stenosis severity and lesion length.

## Does it hold up over a heartbeat?

A time-averaged picture can hide a lot. Blood flow is pulsatile, and the clinically interesting moment is peak systole, when shear is highest and the model has the most to get wrong.

{% include figure.html video="/assets/projects/cardiovascular-super-resolution/cycle-heldout.mp4" poster="/assets/projects/cardiovascular-super-resolution/cycle-heldout-poster.webp" alt="Animation of a held-out healthy coronary geometry: an inflow waveform on the left with a marker riding the cardiac cycle, and three artery trees on the right coloured by wall shear stress — low-resolution input, ML prediction, and high-resolution CFD." caption="The held-out healthy case, through one cardiac cycle. Watch the marker ride the inflow curve on the left: as flow surges, the ML tree lights up the same branches at the same moments as the reference. The pulsatility is recovered, not just the average." %}

Across all four featured geometries, per-node predicted shear tracks the solver at r = 0.92–0.94 — including on the healthy geometry the model was never trained on.

{% include figure.html src="/assets/projects/cardiovascular-super-resolution/correlation.webp" alt="Four hexbin density plots of ML-predicted wall shear stress against CFD wall shear stress, one per geometry, each hugging the 1:1 diagonal with correlation coefficients of 0.94, 0.92, 0.94 and 0.94." caption="Every wall node of four geometries against ground truth. The density collapses onto the 1:1 line in all four, held-out case included." wide=true %}

The measure that actually decides something is high-shear exposure — how much of the wall crosses a clinical threshold, and when. At peak systole the model and the solver agree that roughly 62% and 65% of the wall exceeds 20 dyne·cm⁻². The coarse simulation puts it under 10%, which is not a small error but the opposite finding.

{% include figure.html src="/assets/projects/cardiovascular-super-resolution/hemodynamics.webp" alt="Four panels: time-averaged WSS distribution, TAWSS agreement scatter, spatial WSS over the cardiac cycle, and percentage of wall area above 20 dyne per square centimetre, each comparing low-resolution input, ML prediction and high-resolution CFD." caption="Grey is the coarse run, blue the model, red the solver. Blue tracks red in every panel; grey does not." %}

## Generalizing across anatomy

One set of weights, four coronary trees, bifurcation angles from 68° to 122°. The high-shear bands land where each vessel's own anatomy puts them — on the lesion neck, on the flow dividers — rather than in the same place every time. The model learned the hemodynamics, not a shape.

{% include figure.html video="/assets/projects/cardiovascular-super-resolution/generalization.mp4" poster="/assets/projects/cardiovascular-super-resolution/generalization-poster.webp" alt="Two-by-two animated grid of coronary artery trees labelled healthy held-out, 68 degree, 95 degree and 109 degree bifurcations, coloured by ML-predicted wall shear stress, with a small inflow waveform inset." caption="Four geometries, one model, one shared inflow clock — and a different shear signature in each." %}

## What it costs

Twelve hours of high-fidelity CFD against 20.3 minutes end to end. The interesting detail is the split: 18 minutes 12 seconds of that is the coarse simulation you still have to run, and only 2.08 minutes is the network. The model is no longer the bottleneck — the cheap solver is.

{% include figure.html src="/assets/projects/cardiovascular-super-resolution/cost.webp" alt="Log-scale bar chart comparing time to convergence: a stacked 20.3 minute bar for the ML-accelerated method, of which 18 minutes 12 seconds is the low-resolution simulation and 2.08 minutes the ML prediction, against a 12 hour bar for high-resolution CFD." caption="Log scale, so the bars understate the gap. Measured on CMU's TRACE cluster: 128 cores and one NVIDIA A40." %}

[Talk — APS-DFD 2025, Houston](/publications/#talks) · [Related paper — J. Comput. Phys. 538 (2025)](https://doi.org/10.1016/j.jcp.2025.114131)
{: .inline-links}

[← All projects](/#projects) · [Research overview](/research/#vascular)
{: .project-nav}
