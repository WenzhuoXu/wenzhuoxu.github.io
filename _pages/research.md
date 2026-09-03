---
title: "Research"
permalink: /research/
layout: single
classes: wide
author_profile: false
toc: true
toc_sticky: true
toc_label: "Projects"
read_time: false
share: false
---

I work on making a model's claims about a physical system *checkable*. That has taken two forms. In one, I build agentic systems that take a claim about a physical process — a generated video should obey gravity, a document's equations should close — and reduce it to measurements a person can audit. In the other, at CMU, I build learned surrogates for large-scale simulation, where "checkable" means agreeing with a solver on meshes far larger than anything the model was trained on.

The two are the same problem at different scales: the hard part is never the prediction, it is knowing when to believe it.

## Agentic systems for physical reasoning

Current work, with Tong Sun. Technical reports are in preparation, so the descriptions below stay at the level of approach.

### <a class="site-link" href="https://veriphy-ai.github.io/">VeriPhy: agentic physical reasoning for video evaluation</a> {#veriphy}

<span class="status">technical report in preparation</span>

Video generation models are usually scored with a single number, which tells you a clip is bad without telling you what is wrong with it. VeriPhy reframes evaluation as an **auditable verdict** rather than a score.

A reasoning model compiles the generation prompt into typed physical obligations — the specific commitments the clip has to honour — together with an executable measurement plan. A library of frozen perception operators executes that plan and returns *only measurements*, never judgements. Deterministic rules then compose those measurements into a verdict of **supported**, **contradicted**, or **unknown**, with provenance back to the operator call and time span that produced it. Because "unknown" is a first-class outcome, the system can decline to rule instead of guessing.

Two design commitments do most of the work:

- **Planning beats interrogation.** Compiling the whole prompt into one measurement plan up front recovers substantially more localized flaws than verifying claims one at a time, at a cost of roughly one additional operator call per clip. Checking claims independently misses exactly the flaws that only surface when obligations are measured together.
- **The agent improves by editing a readable state, not by updating weights.** An improvement is a diff to an operator library, a set of distilled plans, failure priors, and a gated external-knowledge channel — something a person can read, review, version, and revert. A candidate edit is accepted only when it improves a held-out score; outside knowledge enters through the same gate, so the loop cannot feed on its own output; and evidence is tagged separately from belief, so a distilled prior is never mistaken for a measurement.

Anchoring the work is a human-annotated flaw benchmark in which each record quotes the exact violated fragment of the prompt, with a rationale, a severity, a time span, and the object track it applies to. That per-claim structure is what makes miss attribution possible at all — a clip-level score can tell you that you were wrong, but not which obligation you failed to check.

{% comment %}
  Quantitative results held back pending disclosure review. To publish,
  clear these figures and fold them back into the text above:
    - benchmark scale: 1,500 clips, 2,582 human flaw records
    - plan-based execution recovered 179 of 295 localized flaws (60.7%) vs.
      135 (45.8%) for one-at-a-time claim verification — a gain of 44 flaws,
      paired bootstrap interval [+29, +59], at one extra operator call/clip
    - operator library: SAM 3 tracking, instance counting, 11 typed motion
      measurements, depth, OCR, audio

  NOTE: this MUST stay a Liquid {% raw %}{% comment %}{% endraw %} block, not an
  HTML <!-- --> comment. kramdown passes HTML comments straight through to the
  published page, so anything in one is readable via View Source.
{% endcomment %}

### Project Still Life: executable physics from static documents {#still-life}

<span class="status">ongoing</span>

A textbook chapter contains a complete physical model, but it is inert: the equations sit on the page and the reader has to reconstruct the system in their head. Still Life turns the physics printed in a document into something you can run.

The pipeline parses both the equations and the prose around them, builds a symbol-binding graph and a document knowledge graph, and then **walks that graph until the equation system closes** — until every symbol is grounded in something the document actually states. The closed system compiles to a typed scenario card and then to an interactive simulation, gated by symbolic and dimensional assertions on units, conservation, and limiting cases. A simulation that cannot pass its own assertions never reaches the reader.

Two pieces support it:

- **A within-document sufficiency benchmark.** The question is not "did retrieval find a relevant passage" but "did it return the complete, self-contained bundle needed to ground every symbol." It is scored on the units that share *zero* tokens with the query, across escalating levels of query noise — precisely the units lexical and embedding retrieval cannot reach. The closure walk reaches them by following symbols rather than words, and unlike agentic retrieval baselines it has a stop condition: it halts when the system closes.
- **A simulation-conditioned generation testbed**, used to measure *when* a video generator commits to a motion. Releasing structural control early preserves an airborne trajectory but not the ground contact that follows — reported as a noise level rather than a step index, so the finding transfers across sampling schedules.

The end-to-end demonstration is an interactive reading experience: click any figure in a chapter and get a playable simulation with what-if controls, with the chapter's own photograph animated by depth-conditioned video generation.

{% comment %}
  Held back pending disclosure review (Liquid comment, not HTML — see the
  note in the VeriPhy section above):
    - benchmark name (FCR-Bench); assertion stack (SymPy, pint)
    - testbed: MuJoCo depth control into Wan 2.2 VACE, 1,314 scenes across
      66 kinds; five levels of query noise
{% endcomment %}

## Scientific machine learning for physical simulation

Ph.D. work at CMU with [Christopher McComb](https://engineering.cmu.edu/directory/bios/mccomb-christopher.html) and [Noelia Grande Gutiérrez](https://www.meche.engineering.cmu.edu/directory/bios/grande-gutierrez-noelia.html), across the [Design Research Collective](https://cmudrc.github.io/) and [BioSiMMlab](https://www.meche.engineering.cmu.edu/faculty/gutierrez-biosimm-lab.html).

### Engineering super-resolution for Autonomous Digital Design {#add}

*Collaboration with Eaton Research Labs and the U.S. Army Engineer Research and Development Center (ERDC).*

Design engineers iterate faster than high-fidelity CFD can run, so the simulation stops being part of the design loop. This project makes a coarse simulation usable as if it were a fine one.

I built a fully parameterized CFD dataset of more than **100,000 flow-field simulations** spanning varying geometries and boundary conditions, and used it to train a super-resolution model that generalizes across that space while holding **under 5% error in the key flow quantities** engineers size hardware against. Applied to three-dimensional duct geometries with graph neural networks and adaptive domain decomposition, it reaches **up to 5.5× speedup** over the equivalent high-resolution numerical simulation.

The method is **deployed in Eaton's jet engine duct system design workflow** — the part I care about most, because a surrogate that never leaves the paper it was published in has not really been tested.

[Project page](/projects/duct-super-resolution/) · [Journal paper (JCISE 2026)](/publications/#flow-conveyance) · [Conference version (IDETC-CIE 2025)](/publications/#duct-idetc)
{: .inline-links}

### Domain decomposition for large-scale physics-informed learning {#domain-decomposition}

*Manufacturing Futures Institute initiative.*

Physics-informed neural networks are elegant and do not scale — the global constraint that makes them work is also what keeps them off a real part. The fix is to enforce the **principle of locality**: a physical element is influenced only by a bounded neighbourhood, so the domain can be decomposed, distributed across GPU nodes, and solved in parallel without giving up the physics. That matters for industrial use, where the constraint is wall-clock time.

This is the **first ML method to scale PINNs past 3 million physical elements**. Against high-fidelity reference simulations it reaches **99.47% R² in velocity and 99.96% in pressure**, and it beats traditional FEM solvers on time-to-solution while holding accuracy. I also proposed a **spectrum encoding** for measuring domain shift across physics regimes — a way to ask whether a model trained on one regime has any business being applied to another, before finding out the expensive way.

The method is deployed in two very different settings: metal additive manufacturing and cardiovascular simulation.

[Project page](/projects/adaptive-domain-decomposition/) · [Locality paper (JCP 2025)](/publications/#locality) · [Additive manufacturing application (JMSE 2024)](/publications/#fno-am-journal)
{: .inline-links}

### Graph neural operator super-resolution for vascular hemodynamics {#vascular}

*BioSiMMlab, with clinical collaborators.*

Wall shear stress is the quantity clinicians want out of a cardiovascular flow simulation, and it is exactly the quantity a coarse mesh gets wrong. This project super-resolves patient-specific vascular flow well enough for that number to be trusted.

I developed a discrete formulation of TEECNet using a **branch–trunk architecture with a Taylor-series expansion on bounded velocity proxies**, predicting high-resolution velocity fields and wall shear stress directly on unstructured vascular meshes. Three pieces make it work on real patient geometry rather than idealized vessels:

- **Physics-aware adaptive sampling**, weighted by velocity-gradient magnitude, surface curvature, and wall proximity, so resolution is spent where the flow is actually doing something.
- **Velocity-directed inlet detection** for automatic rigid-body coordinate alignment between patient geometries. It handles stenotic and diseased cases where magnitude-based methods fail — and those are the cases that matter clinically.
- A **wall-proximity-weighted loss** that prioritizes near-wall node accuracy, because near-wall error is what corrupts a clinical wall-shear-stress estimate.

The clinical arm of this work is 4D flow MRI enhancement: anatomy-aware machine learning for 4D flow MRI, aimed at improving management of cardiovascular disease such as bicuspid aortic valve (BAV) by producing real-time, accurate, patient-specific flow fields and the hemodynamic metrics that inform a decision.

[Project page](/projects/cardiovascular-super-resolution/) · [Talk (APS-DFD 2025)](/publications/#talks)
{: .inline-links}

### TEECNet and MegaFlow2D {#teecnet-megaflow}

The method and the dataset everything above is built on.

**TEECNet** learns the *discretization error* between a low- and a high-fidelity simulation instead of learning the solution field. That is the whole idea: the error is a smaller, smoother, more local object than the field itself, so a coarse mesh can be corrected up to fine-mesh accuracy for a fraction of the cost of actually running the fine mesh. It operates on graph representations, which is what lets it take irregular meshes and complex geometry as they come, and respect boundary conditions, rather than requiring everything be resampled onto a grid first.

**MegaFlow2D** exists because the comparison was not possible before it. Every super-resolution method was being reported on its own bespoke flow, so nothing was commensurable. It is a parametric dataset that puts architectures for fluid flow prediction and enhancement on common ground.

[Project page](/projects/teecnet/) · [TEECNet code](https://github.com/cmudrc/TEECNet) · [MegaFlow2D dataset](https://github.com/cmudrc/MegaFlow2D) · [TEECNet (JCP 2025)](/publications/#teecnet) · [MegaFlow2D (CPS-IoT Week 2023)](/publications/#megaflow2d)
{: .inline-links}
