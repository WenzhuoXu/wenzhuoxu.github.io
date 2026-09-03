---
title: "CV"
permalink: /cv/
layout: single
classes: wide
author_profile: false
toc: true
toc_sticky: true
toc_label: "Contents"
read_time: false
share: false
---

{%- assign cv_pdf = site.static_files | where: "path", "/assets/Wenzhuo_Xu_CV.pdf" | first -%}
{%- if cv_pdf %}
[Download CV (PDF)](/assets/Wenzhuo_Xu_CV.pdf) — updated {{ cv_pdf.modified_time | date: "%B %Y" }}.
{: .cv-download}
{%- else %}
{% comment %}
  Drop a PDF export at assets/Wenzhuo_Xu_CV.pdf and the download link appears
  automatically, dated from the file's own timestamp. Nothing else needs
  editing. Strip the phone number from the CV header first — this page is
  public and indexed.
{% endcomment %}
{%- endif %}

## Experience

### Research Scientist Intern — Adobe Research

*May 2026 – present · with Tong Sun and Jiuxiang Gu*

- **[VeriPhy](/research/#veriphy)** — agentic physical reasoning for video evaluation. Core contributor; technical report in preparation.
- **[Project Still Life](/research/#still-life)** — executable physics from static documents. Core contributor.

### Graduate Research Assistant — Carnegie Mellon University

*October 2022 – present · Department of Mechanical Engineering · advised by Christopher McComb and Noelia Grande Gutiérrez*

- **[Engineering super-resolution for Autonomous Digital Design](/research/#add)** — parameterized CFD dataset of 100,000+ simulations; generalizable super-resolution holding under 5% error in key flow quantities; deployed in Eaton's jet engine duct system design workflow.
- **[Domain decomposition for large-scale physics-informed learning](/research/#domain-decomposition)** — first ML method scaling PINNs past 3 million physical elements; spectrum encoding for measuring domain shift across physics regimes; deployed to metal additive manufacturing and cardiovascular simulation.
- **[Graph neural operator super-resolution for vascular hemodynamics](/research/#vascular)** — discrete TEECNet formulation predicting high-resolution velocity fields and wall shear stress on unstructured vascular meshes, including the 4D flow MRI clinical arm.

Collaborations: Eaton Research Labs, U.S. Army ERDC, Manufacturing Futures Institute.
{: .cv-note}

### Undergraduate Research Assistant — Shanghai Jiao Tong University

*April 2019 – June 2022 · combustion diagnostics and computational mechanics*

- High-speed photography of turbulent flame dynamics with ML flame-front prediction reaching 89% accuracy. Center for Combustion and Environmental Technology, with Prof. Lei Zhu.
- FEM analysis of ultrasonic wave propagation in composite materials, during a three-month research internship at the Laboratoire d'Acoustique de l'Université du Mans (LAUM), Le Mans Université, January – March 2021, with Prof. Vitali Goussev.

## Teaching

- **Teaching Assistant**, 24-261 Mechanics I (undergraduate) — Carnegie Mellon University, Fall 2024
- **Teaching Assistant**, 24-718 Computational Fluid Dynamics (graduate) — Carnegie Mellon University, Fall 2023
- **Teaching Assistant**, Chassis and Powertrain Design for Automobiles (undergraduate) — Shanghai Jiao Tong University, Spring 2021
{: .cv-list}

## Awards and honors

- **Milton Shaw Ph.D. Research Award**, Carnegie Mellon University — 2023<br>
  <span class="cv-sub">Awarded for excellence in mechanical engineering research.</span>
- **Graduate with Honors**, Shanghai Jiao Tong University — 2022<br>
  <span class="cv-sub">Graduated with distinction from the School of Mechanical Engineering.</span>
- **Second Prize, Formula Student China** — 2022<br>
  <span class="cv-sub">Member of the SJTU racing team that designed and built a formula-style race car.</span>
- **Distinguished Conference Paper**, SAECCE (Society of Automotive Engineers of China – Congress and Exhibition) — 2020<br>
  <span class="cv-sub">Recognized for outstanding contribution to automotive engineering research.</span>
- **Merit-based scholarships**, Shanghai Jiao Tong University — 2018–2022<br>
  <span class="cv-sub">Multiple merit-based scholarships throughout undergraduate studies.</span>
{: .cv-list}

## Professional service

**Peer reviewer** — IEEE/ASME Transactions on Mechatronics · Journal of Mechanical Design
{: .cv-note}

**Memberships** — Association for Computing Machinery (ACM) · American Society of Mechanical Engineers (ASME) · American Physical Society (APS) · American Heart Association (AHA)
{: .cv-note}

## Technical skills

**Machine learning** — vision–language models and agentic LLM systems · diffusion-based video generation · neural operators · graph neural networks · physics-informed neural networks · deep learning for scientific computing
{: .cv-note}

**Computational methods** — custom numerical solvers for flow simulation · finite element method (FEM) implementation · computational fluid dynamics · turbulence modeling
{: .cv-note}

**High-performance computing** — parallel GPU programming · Bridges-2, TRACE and other supercomputing clusters · large-scale data processing · distributed computing
{: .cv-note}

**Software** — Python · C++ · MATLAB · PyTorch · FEniCS · MuJoCo · ANSYS · COMSOL Multiphysics · SolidWorks · CATIA · Git
{: .cv-note}

## Education

- **Ph.D., Mechanical Engineering** — Carnegie Mellon University, expected May 2027. Advised by Christopher McComb and Noelia Grande Gutiérrez.
- **M.S., Mechanical Engineering** — Carnegie Mellon University, August 2024. Earned en route to the Ph.D.
- **B.Eng., Mechanical Engineering & B.A., German** — Shanghai Jiao Tong University, June 2022. Dual-degree program.
{: .cv-list}
