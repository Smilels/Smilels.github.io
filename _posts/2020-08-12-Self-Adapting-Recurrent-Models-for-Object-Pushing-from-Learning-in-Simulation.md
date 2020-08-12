---
layout: post
title: "Self-Adapting Recurrent Models for Object Pushing from Learning in Simulation"
date: 2020-08-12
---

<div align="center">
[Lin Cong](https://tams.informatik.uni-hamburg.de/people/cong/), [Michael Görner](https://tams.informatik.uni-hamburg.de/people/goerner/), [Philipp Ruppel](https://tams.informatik.uni-hamburg.de/people/ruppel/), [Hongzhuo Liang](https://tams.informatik.uni-hamburg.de/people/liang/), [Norman Hendrich](https://tams.informatik.uni-hamburg.de/people/hendrich/), [Jianwei Zhang](https://tams.informatik.uni-hamburg.de/people/zhang/)
</div>

Planar pushing remains a challenging research topic, where building the dynamic model of the interaction is the core issue.
Even an accurate analytical dynamic model is inherently unstable because
physics parameters such as inertia and friction can only be approximated.
Data-driven models usually rely on large amounts of training data,
but data collection is time consuming when working with real robots.

In this paper, we collect all training data in a physics simulator and build an LSTM-based model to fit the pushing dynamics.
Domain Randomization is applied to capture the pushing trajectories of a generalized class of objects.
When executed on the real robot, the trained recursive model adapts
to the tracked object's real dynamics within a few steps.
We propose the algorithm Recurrent Model Predictive Path Integral (RMPPI) as a variation of the original MPPI approach,
employing state-dependent recurrent models.
