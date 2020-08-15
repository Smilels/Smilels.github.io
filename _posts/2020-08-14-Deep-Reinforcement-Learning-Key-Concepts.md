---
layout: post
title: "Reinforcement Learning Key Concepts"
data: 2020-08-12
---

> Reinforcement Learning has long been a popular research topic in ML field, but the practical application value of early RL algorithm is always limited by computation resources and function approximation methods. As deep learning thrives, deep reinforcement learning combines deep network and RL principles in one framework. The come out of [AlphaGo](https://deepmind.com/blog/article/alphago-zero-starting-scratch), an algorithm that beats the human world champion, broadens people's horizon and open up an exciting research area.
In this blog, I will try to elaborate some key concepts in RL which caused confusion during my initial learning process. Hope it can help you to some degree. Most of the concepts and notes in this blog are from [OpenAI Spinning Up](https://spinningup.openai.com/en/latest/index.html), which is a very concrete tutorial for RL starters.

## Determined Policy and Stochastic Policy
A policy is the control rule to decide the actions to take according to current environment situations. It can be deterministic, in which case it is usually denoted by $$ \mu: $$

$$ a_t = \mu(s_t) $$
or it may be stochastic, in which case it is usually denoted by $$\pi:$$

$$ a_t \sim \pi(\cdot | s_t)$$
We often denote the parameters of such policy by $$\theta$$ or $$\phi$$

$$ a_t = \mu_{\theta}(s_t) $$

$$ a_t \sim \pi_{\theta}(\cdot | s_t)$$

The concept of determined policy is straight forward. Stochastic policies in deep RL can be divided into **categorical policies** and **diagonal Gaussian policies**. Categorical policies can be used in discrete action spaces, while diagonal Gaussian policies are used in continuous action spaces.

### Categorical Policies
A categorical policy is like a classifier over discrete actions. You build the neural network for a categorical policy the same way you would for a classifier: the input is the observation, followed by some number of layers (possibly convolutional or densely-connected, depending on the kind of input), and then you have one final linear layer that gives you logits for each action, followed by a softmax to convert the logits into probabilities.

**Sampling:**

Given the probabilities for each action, frameworks like PyTorch and Tensorflow have built-in tools for sampling.

**Log-Likelihood:**

$$ \log \pi_{\theta}(a|s) = \log [P_{\theta}(s)]_{a} $$

### Diagonal Gaussian Policies
A multivariate Gaussian distribution (or multivariate normal distribution, if you prefer) is described by a mean vector, \mu, and a covariance matrix, \Sigma. A diagonal Gaussian distribution is a special case where the covariance matrix only has entries on the diagonal. As a result, we can represent it by a vector.

**Sampling:**

Given the mean action $$\mu_{\theta}(s)$$ and standard deviation $$\sigma_{\theta}(s)$$, and a vector z of noise from a spherical Gaussian $$(z \sim \mathcal{N}(0, I))$$, an action sample can be computed with
$$ a = \mu_{\theta}(s) + \sigma_{\theta}(s) \odot z $$

**Log-Likelihood:**

The log-likelihood of a k -dimensional action a, for a diagonal Gaussian with mean $$\mu = \mu_{\theta}(s)$$ and standard deviation $$\sigma = \sigma_{\theta}(s)$$, is given by

$$ \log \pi_{\theta}(a|s) = -\frac{1}{2}\left(\sum_{i=1}^k \left(\frac{(a_i - \mu_i)^2}{\sigma_i^2} + 2 \log \sigma_i \right) + k \log 2\pi \right) $$


## Value Functions

It’s often useful to know the value of a state, or state-action pair. By value, we mean the expected return if you start in that state or state-action pair, and then act according to a particular policy forever after. There are four main functions of note here.

**The On-Policy Value Function**, $$V^{\pi}(s)$$, which gives the expected return if you start in state s and always act according to policy $$\pi$$:

$$V^{\pi}(s) = \underset{\tau \sim \pi}{E}[R(\tau)| s_0 = s]$$

**The On-Policy Action-Value Function**, $$Q^{\pi}(s,a)$$, which gives the expected return if you start in state s, take an arbitrary action a (which may not have come from the policy), and then forever after act according to policy $$\pi$$:

$$Q^{\pi}(s,a) = \underset{\tau \sim \pi}{E}[R(\tau)| s_0 = s, a_0 = a]$$

**The Optimal Value Function**, $$V^*(s)$$, which gives the expected return if you start in state s and always act according to the optimal policy in the environment:

$$ V^*(s) = \max_{\pi} \underset{\tau \sim \pi}{E}[R(\tau)| s_0 = s] $$

**The Optimal Action-Value Function**, $$Q^*(s,a)$$, which gives the expected return if you start in state s, take an arbitrary action a, and then forever after act according to the optimal policy in the environment:

$$Q^*(s,a) = \max_{\pi} \underset{\tau \sim \pi}{E}[R(\tau)| s_0 = s, a_0 = a]$$

## Bellman Equations

> The value of your starting point is the reward you expect to get from being there, plus the value of wherever you land next.

The Bellman equations for the on-policy value functions are:

$$V^{\pi}(s) = \underset{s'\sim P}{\underset{\tau \sim \pi}{E}}[r(s,a) + \gamma V^{\pi}(s')]$$

and:

$$Q^{\pi}(s,a) = \underset{s'\sim P}{E}[r(s,a) + \gamma \underset{a' \sim \pi}{E}[Q^{\pi}(s',a')]]$$
## Advantage Functions

The advantage function $$A^{\pi}(s,a)$$ corresponding to a policy $$\pi$$ describes how much better it is to take a specific action $$a$$ in state $$s$$, over randomly selecting an action:

$$A^{\pi}(s,a) = Q^{\pi}(s,a) - V^{\pi}(s)$$
