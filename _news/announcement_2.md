---
layout: post
title: New preprint
date: 2021-08-01 16:11:00+0200
inline: false
---

We have uploaded a research paper titled "Numerical wave propagation aided by deep learning" to ArXiv.
You can check it out <a href="https://arxiv.org/abs/2107.13184"> here <a>. Here is the abstract.

***

We propose a deep learning approach for wave propagation in media with multiscale wave speed, using a second-order linear wave equation model. 
We use neural networks to enhance the accuracy of a given inaccurate coarse solver, which under-resolves a class of multiscale wave media and wave fields of interest. 
Our approach involves generating training data by the given computationally efficient coarse solver and another sufficiently accurate solver, applied to a class of wave media 
(described by their wave speed profiles) and initial wave fields. 
We find that the trained neural networks can approximate the nonlinear dependence of the propagation on the wave speed as long as the causality is a
ppropriately sampled in training data. We combine the neural-network-enhanced coarse solver with the parareal algorithm and demonstrate that the coupled approach improves the stability of parareal algorithms for wave propagation and improves the accuracy of the enhanced coarse solvers.

***