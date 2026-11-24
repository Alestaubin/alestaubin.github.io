---
permalink: /
title: "Welcome"
author_profile: true
redirect_from: 
  - /about/
  - /about.html
---

## About Me

I am a MSc student in Computer Science at the University of British Columbia, supervised by Professor [Evan Shelhamer](https://imaginarynumber.net). Prior to this, I completed a Joint Honours BSc in Mathematics and Computer Science at McGill University.

Beyond academia, I like to call myself a photographer (see my work [here](https://alexstaubinphoto.com)), and I try my best at cycling. Combining the two makes for a very happy me. I also enjoy hiking and I've been trying to climb as many mountains as I can during my time in British Columbia.

## News

{% for item in site.data.news %}
- **{{ item.date }}**: {{ item.text }}
{% endfor %}

## Research Interests

My research sits at the intersection of **deep learning**, **computer vision**, and **robotics**, with a focus on **robustness and adaptation**. A core challenge in deploying learned systems in the real world is distribution shift, i.e. the gap between the data a model is trained on and the conditions it encounters at test time. I am broadly interested in understanding and closing this gap.

Concretely, I'm interested in:

- **Domain Adaptation for Vision**: Developing methods that allow vision systems to adapt to new environments with little or no labelled target data. This includes both traditional domain adaptation settings and the more challenging continual or online adaptation regimes.

- **Robust Control Policies for Robotics**: Extending robustness questions into the control setting. Specifically, how do we train robot policies via imitation or reinforcement learning that remain reliable when the visual observation distribution shifts at deployment? Sim-to-real transfer and policy robustness to perceptual perturbations are of particular interest.

The common thread across these directions is the question: *how do we build systems that know what they don't know, and adapt gracefully when the world changes?*

## Selected Publications

{% include selected-pubs.html %}

## Background & Past Work

During my undergrad I explored two distinct threads:

- **Robotics**: I worked on imitation learning for long-horizon manipulation tasks, aiming to make robotic behaviour more capable and generalizable.
- **AI & Society**: I investigated the societal impacts of AI, specifically the effects of deepfakes on electoral integrity in U.S. elections.