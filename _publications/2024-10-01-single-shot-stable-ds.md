---
title: "Single-Shot Learning of Stable Dynamical Systems for Long-Horizon Manipulation Tasks"
collection: publications
category: publications
selected: true
permalink: /publication/2024-10-01-Single-shot
authors: 'Alexandre St-Aubin, Amin Abyaneh, Hsiu-Chin Lin'
excerpt: 'Segmenting long-horizon demonstrations into subgoals and learning globally stable dynamical-system policies for each, with sim-to-real validation.'
date: 2024-10-01
venue: 'arXiv preprint arXiv:2410.01033'
arxivurl: 'https://arxiv.org/abs/2410.01033'
paperurl: 'https://alestaubin.github.io/files/2410.01033v2.pdf'
bibtexurl: 'https://alestaubin.github.io/files/bibtex1.bib'
---
Mastering complex sequential tasks continues to pose a significant challenge in robotics. While there has been progress in learning long-horizon manipulation tasks, most existing approaches lack rigorous mathematical guarantees for ensuring reliable and successful execution. In this paper, we extend previous work on learning long-horizon tasks and stable policies, focusing on improving task success rates while reducing the amount of training data needed. Our approach introduces a novel method that (1) segments long-horizon demonstrations into discrete steps defined by waypoints and subgoals, and (2) learns globally stable dynamical system policies to guide the robot to each subgoal, even in the face of sensory noise and random disturbances. We validate our approach through both simulation and real-world experiments, demonstrating effective transfer from simulation to physical robotic platforms.