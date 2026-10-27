---
title: "Dynamic Duos: Robust Duo Adaptation Under Shift"
collection: publications
category: projects
permalink: /publication/202605-dynamic-duos-aicrv
excerpt: 'Pairing a large and a small model and adapting them jointly for robustness under distribution shift. Poster at AI/CRV 2026.'
date: 2026-05-25
venue: 'Canadian Conference on AI, Robots & Vision (AI/CRV) 2026, SFU (poster)'
posterurl: 'https://alestaubin.github.io/files/Dynamic_Duos_Poster_AICRV2026.pdf'
---
*Alexandre St-Aubin and Evan Shelhamer. University of British Columbia, Vector Institute.*

This is the first iteration of Dynamic Duos, presented as a poster at AI/CRV 2026 at Simon Fraser University.

## Asymmetric Duos

An Asymmetric Duo pairs a large model with a much cheaper small model and combines their predictions through joint temperature scaling. This costs only slightly more than a single model, while a deep ensemble costs many times more. An oracle sweep over 231 pairs of torchvision architectures selects ViT-B/16 + ResNet-50 as the best duo (+1.4 pp over the best single model).

## The problem: fixed temperatures fail under shift

Temperatures calibrated on clean data cannot adapt. The optimal temperatures vary drastically across ImageNet-C corruptions, and on some shifts the best strategy is to suppress the small model entirely. At severity 5, the duo with clean-fitted temperatures (0.375) falls below ViT-B/16 alone (0.393). Refitting on a mix of clean and held-out corrupted data closes roughly 75% of the gap to the per-corruption oracle, but a single global pair of temperatures still cannot tell noisy images from blurred ones.

## Method 1: Joint Temperature Network

A small MLP predicts per-sample temperatures for both models from their frozen penultimate features, with no gradient computation at test time. It is initialized from the fixed calibrated temperatures and regularized so it cannot degrade catastrophically. Fixed temperature scaling plateaus near 0.437 mean accuracy as more corrupted training data is added, while the JointTempNet keeps improving (up to +1.4 pp with 10k samples per corruption).

## Method 2: Duo Test-Time Adaptation

Following TENT, we minimize the entropy of the duo's *joint* prediction at test time, updating only the affine parameters of normalization layers. Routing adaptation through the joint entropy, rather than each model's own entropy, is far more stable:

- Duo + Joint TENT reaches 0.656 mean accuracy across ImageNet-C at severity 5, compared to 0.375 for the duo with fixed temperatures and 0.374 for TENT on the large model alone.
- Single-model TENT can collapse on unseen shifts (e.g. Fog with the large model: 0.487 to 0.056), while Joint TENT stays stable and improves over both models on every corruption tested.
- The second model acts as an anchor that pulls predictions away from degenerate solutions. Both models must fail at the same time for the duo to collapse.
