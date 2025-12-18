---
title: "Single-Shot Learning of Stable Dynamical Systems for Long-Horizon Manipulation Tasks"
collection: publications
category: projects
permalink: /publication/2024-10-01-Single-shot
excerpt: 'This paper is about defining a heuristic approach to segment long-horizon manipulation tasks in robotics.'
date: 2024-10-01
#venue: 'McGill University'
slidesurl: #'https://academicpages.github.io/files/slides1.pdf'
paperurl: 'https://academicpages.github.io/files/2410.01033v2.pdf'
bibtexurl: 'https://academicpages.github.io/files/bibtex1.bib'
citation: #'St-Aubin, Alexandre. (2025). &quot;Paper Title Number 1.&quot; <i>Journal 1</i>. 1(1).'
---
Mastering complex sequential tasks continues to pose a significant challenge in robotics. While there has been progress in learning long-horizon manipulation tasks, most existing approaches lack rigorous mathematical guarantees for ensuring reliable and successful execution. In this paper, we extend previous work on learning long-horizon tasks and stable policies, focusing on improving task success rates while reducing the amount of training data needed. Our approach introduces a novel method that (1) segments long-horizon demonstrations into discrete steps defined by waypoints and subgoals, and (2) learns globally stable dynamical system policies to guide the robot to each subgoal, even in the face of sensory noise and random disturbances. We validate our approach through both simulation and real-world experiments, demonstrating effective transfer from simulation to physical robotic platforms.