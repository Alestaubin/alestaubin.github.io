---
title: "Dynamic Duos for Reliable Test-Time Adaptation: Two Models are Better than One"
collection: publications
category: publications
selected: true
permalink: /publication/dynamic-duos
redirect_from:
  - /publication/202605-dynamic-duos-aicrv
  - /publication/202611-dynamic-duos-cssrc
authors: 'Alexandre St-Aubin, Evan Shelhamer'
excerpt: 'Pairing a large model with a small sidekick and adapting them at test time, with a label-free gate that routes away from a member when adaptation makes it collapse. Earlier stages presented at AI/CRV 2026 (poster) and CSSRC 2026 (talk).'
date: 2026-11-14
venue: 'Under review'
# posterurl: 'https://alestaubin.github.io/files/Dynamic_Duos_Poster_AICRV2026.pdf'
# slidesurl: 'https://alestaubin.github.io/files/Dynamic_Duos_Slides_CSSRC2026.pdf'
---
<!-- *Alexandre St-Aubin and Evan Shelhamer. University of British Columbia, Vector Institute.* -->

## Abstract

Test-time adaptation (TTA) updates a model on unlabeled test data to improve accuracy under distribution shift. 
However, a major obstacle to deploying TTA is that it can also reduce accuracy, and most TTA methods give no signal of failure. 
We show how to adapt Asymmetric Duos, which pair a larger model with a smaller model, for more reliable adaptation with minimal overhead.
We find that a Duo is already more robust than its members even without adaptation. 
Adapting both members of the Duo can raise accuracy further, but one model can collapse while the other stays accurate, and the Duo's fixed combination keeps trusting both. 
We propose _Dynamic Duos_, which replace the Duo's fixed combination with a gate that re-weights the members on every batch using a label-free reliability estimate. 
We extend gating to resetting by using the same estimate to restore a collapsed member to its source weights while its partner keeps adapting.
Dynamic Duos are compatible with any TTA update rule.
On ImageNet-C with Tent, Dynamic Duos help where adaptation fails and do no harm where it succeeds. They improve accuracy by 5.5 points over a fixed combination for an adapting ViT-B/16 + ConvNeXt Duo whose small member collapses. 
On continual ImageNet-C, _Dynamic Duos that Reset_ outperform or match scheduled resets and other baselines on all settings we evaluate.

## Project timeline

The full paper is currently under review. It grew out of two earlier, work-in-progress stages:

### November 2026: a gate that survives collapse (CSSRC 2026, talk)

*Presented at CSSRC 2026, a peer-reviewed student conference at UBC.* [Slides](/files/Dynamic_Duos_Slides_CSSRC2026.pdf)

This short project showed that a label-free gate can re-weight the two members on every batch. Each member gets a reliability score: the normalized nuclear norm of its batch softmax matrix. The score is high only when predictions are both **confident** and **dispersed** across classes, so collapse (confident but not dispersed) scores low. A soft gate turns the score gap into weights:

$$w_t^{(L)} = \sigma\big(\beta\,(s_t^{(L)} - s_t^{(S)})\big), \qquad w_t^{(S)} = 1 - w_t^{(L)}$$

Only the gap matters, so a shift that hurts both members equally moves no weight. In a stress test on ImageNet-C (severity 5, Tent with deliberately high learning rates), the gate raised average accuracy from 46.7% (fixed duo) to **51.3%**. It gained about 20 points on fog and snow, where the ViT collapses, and lost at most 0.8 points where no member degrades.

### May 2026: first iteration (AI/CRV 2026, poster)

*Poster at the Canadian Conference on AI, Robots & Vision, Simon Fraser University.* [Poster](/files/Dynamic_Duos_Poster_AICRV2026.pdf)

The first iteration showed that temperatures calibrated on clean data cannot adapt to shift: at severity 5, the duo with clean-fitted temperatures (37.5%) fell below ViT-B/16 alone (39.3%). It explored two fixes:

- **Joint Temperature Network:** a small MLP predicts per-sample temperatures for both models from their frozen features. It keeps improving with more corrupted training data, while fixed temperature scaling plateaus.
- **Duo test-time adaptation:** minimizing the entropy of the duo's *joint* prediction, rather than each model's own, is far more stable. Joint Tent reached 65.6% mean accuracy across ImageNet-C at severity 5, versus 37.4% for Tent on the large model alone. The second model acts as an anchor: both must fail at once for the duo to collapse.
