---
title: "Adaptive local domain decomposition"
permalink: /projects/adaptive-domain-decomposition/
layout: single
classes: wide
author_profile: false
read_time: false
share: false
---

Carnegie Mellon University · with Eaton Research Labs, ERDC and NSF ACCESS · 2024 · presented at APS-DFD 2024, Salt Lake City
{: .project-meta}

<div class="project-hero" markdown="0">
<img src="/assets/projects/adaptive-domain-decomposition/hero.webp" alt="A transitional boundary layer predicted by the model, rendered in yellow and purple, above its absolute-difference field which is almost uniformly dark.">
</div>

A real flow is not one kind of physics. Near the wall it is laminar and orderly; a little further along it trips and breaks down; out in the free stream it is isotropic turbulence. A single network trained across all of that has to be a generalist, and generalists are mediocre everywhere — the loss averages over regimes that want different things from the model, and the compromise satisfies none of them.

The other half of the problem is size. The cost of a learned surrogate scales with the domain the way the solver's does, so the model that worked beautifully on a benchmark box falls over on an engineering part.

<div class="stat-strip" markdown="0">
  <span class="stat"><span class="stat__value">0.66 → 0.80+</span><span class="stat__label">R² after 20 rollout steps, undecomposed vs. decomposed</span></span>
  <span class="stat"><span class="stat__value">3</span><span class="stat__label">physics regimes routed to their own sub-model</span></span>
</div>

## Locality is the licence to cut

The reason you are allowed to chop a domain up at all is that physical systems are local: two points close together are coupled far more strongly than two points far apart. An upwind scheme encodes this in its CFL condition; a spectral method encodes it in sparsity. If locality holds, then a subdomain plus a modest halo contains nearly everything needed to predict its interior — and the pieces can be distributed across GPUs without the physics noticing.

Testing that premise was its own piece of work. Enforcing bounded dependency areas in neural-operator propagation improves both error and learning dynamics — locality is not a compromise you accept for scale, it is a better way to build the model.

{% include figure.html src="/assets/projects/adaptive-domain-decomposition/locality.webp" alt="Panels of isotropic turbulence velocity fields with corresponding error maps, alongside a plot of error against dependency window size." caption="From the locality study I co-authored (Chen, Xu et al., *J. Comput. Phys.* 538, 2025): bounding how far information travels through the network improves accuracy rather than costing it." wide=true %}

## Describe the physics, then route it

If the domain is going to be cut anyway, the pieces need not all go to the same model. The question is how to tell which piece is which — and the answer has to come from the field itself, not from where the piece happens to sit.

{% include figure.html src="/assets/projects/adaptive-domain-decomposition/domain.webp" alt="A wide velocity-magnitude field of a boundary layer with three small sampling boxes marked at different streamwise positions." caption="One simulation, three sample locations: orderly near the inlet, breaking down in the middle, fully turbulent downstream." %}

{% include figure.html src="/assets/projects/adaptive-domain-decomposition/patches.webp" alt="Three small square patches of velocity field extracted from the boundary layer, visibly different in texture." caption="The same three subdomains pulled out on their own. To a network these are three different problems wearing the same units." %}

Each subdomain gets a descriptor and the descriptors get clustered, so the assignment is unsupervised — nobody labels a patch "turbulent". Two descriptions were tried: the subdomain's energy spectrum, and a PCA encoding of the field. Each was clustered under both a Euclidean and a Wasserstein metric.

{% include figure.html src="/assets/projects/adaptive-domain-decomposition/spectrum.webp" alt="Energy spectra plotted for three decomposed locations, normalized energy level against wavenumber, with visibly different slopes." caption="Energy spectra at the three locations. The slopes differ enough to separate regimes without anyone labelling anything." %}

PCA with a Wasserstein metric characterized the physics best — Wasserstein compares whole distributions rather than points, which is the right instrument when what distinguishes two subdomains is the *shape* of their energy content.

{% include figure.html src="/assets/projects/adaptive-domain-decomposition/characterization.webp" alt="Rollout accuracy curves comparing four characterization strategies: PCA with k-means, PCA with Wasserstein, spectrum with k-means, and spectrum with Wasserstein." caption="The four descriptor–metric combinations, compared over a rollout. How you describe a subdomain changes what the routed models learn." %}

## What it bought

The test that matters for a surrogate is recurrent prediction: feed the model its own output and see how long it stays honest. Over twenty steps an undecomposed model decays to R² ≈ 0.66. The decomposed models hold above 0.80 — and the gap widens the further out you predict, which is exactly the direction you want it to run.

{% include figure.html src="/assets/projects/adaptive-domain-decomposition/rollout.webp" alt="R² score against time step for three configurations — three segments, two segments, and no segmentation — over twenty steps, with the unsegmented curve decaying fastest." caption="Twenty steps of recurrent prediction. The undecomposed model falls away; the decomposed ones do not." %}

Look back at the hero figure with that in mind. The prediction panel is a transitional boundary layer mid-breakdown — the hardest thing on this page for a single model to cover — and the error panel below it stays close to zero right through the transition.

[Paper — J. Comput. Phys. 538 (2025)](https://doi.org/10.1016/j.jcp.2025.114131) · [Talk — APS-DFD 2024](/publications/#talks)
{: .inline-links}

[← All projects](/#projects) · [Research overview](/research/#domain-decomposition)
{: .project-nav}
