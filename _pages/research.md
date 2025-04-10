---
title: Research
layout: single
permalink: /research/
author_profile: true
---

## Research Focus

My research focuses on developing advanced machine learning methods for computational fluid dynamics (CFD) problems, with a particular emphasis on super-resolution techniques for multi-scale flows. By integrating physics-based understanding with data-driven approaches, I work to create scalable solutions that address complex engineering challenges across multiple domains. I work at the intersection of scientific computing, deep learning, and fluid mechanics.

## Key Research Areas

### Super-Resolution Analysis for Fluid Dynamics

I develop graph neural network-based approaches to enhance the resolution and accuracy of fluid dynamics simulations. My work on [Taylor Expansion Error Correction Network (TEECNet)](/publications/) provides a framework for super-resolving partial differential equation solutions by learning the discretization error between low and high-fidelity simulations. This approach enables high-accuracy solutions at a fraction of the computational cost of traditional fine-grid simulations.

### Adaptive Domain Decomposition

To overcome computational limitations in large-scale simulations, my research implements innovative domain decomposition techniques that enforce the principle of locality in physical systems. This approach allows for efficient parallel processing across GPU nodes while maintaining high accuracy, making it suitable for industrial applications where time constraints are critical. My recent work has demonstrated up to 99.47% R² accuracy in velocity and 99.96% in pressure compared with high-fidelity simulations.

### Graph Neural Networks for Engineering Applications

I utilize graph representations to capture complex geometries and physical interactions in engineering simulations. My work demonstrates how graph neural networks can effectively learn from irregular mesh structures while preserving physical laws and boundary conditions. This includes the [MegaFlow2D dataset](/publications/), which facilitates the development and evaluation of neural network architectures for fluid flow prediction and enhancement.

## Current Projects

### Fast Super-Resolution Analysis of Low-Pressure Duct Air Flow

This project applies adaptive domain decomposition methods to complex three-dimensional geometries using graph neural networks. The approach significantly reduces computational overhead while maintaining simulation accuracy, achieving up to 5.5× speedup compared to high-resolution numerical simulations.

### 4D Flow MRI Enhancement for Cardiovascular Applications

Working with clinical collaborators, I'm developing anatomy-aware machine learning methods for 4D flow MRI, aiming to improve the clinical management of cardiovascular diseases like bicuspid aortic valve (BAV). This research seeks to provide real-time, accurate patient-specific flow fields and clinically relevant hemodynamic metrics for improved clinical decision-making.

### Physics-Informed Domain Decomposition

Expanding on my work with the principle of locality, I'm investigating how multi-scale physics phenomena can be efficiently learned through physics-informed domain segmentation. This approach aims to capture complex physical behaviors while optimizing computational resources and enabling real-time inference for large-scale engineering applications.
