---
layout: post
title: "On going work, attention mechanism for reinforcement learning"
data: 2020-08-12
---

> Reinforcement Learning has long been a popular research topic in ML field, but the practical application value of early RL algorithm is always limited by computation resources and function approximation methods. As deep learning thrives, deep reinforcement learning combines deep network and RL principles in one framework. The come out of [AlphaGo](https://deepmind.com/blog/article/alphago-zero-starting-scratch), an algorithm that beats the human world champion, broadens people's horizon and open up an exciting research area.
In this blog, I will try to elaborate some key concepts in RL which caused confusion during my initial learning process. Hope it can help you to some degree.

# Determined Policy and Stochastic Policy
A policy is the control rule to decide the actions to take according to current environment situations. It can be deterministic, in which case it is usually denoted by $$ \mu: $$
$$
a_t = \mu(s_t)
$$
