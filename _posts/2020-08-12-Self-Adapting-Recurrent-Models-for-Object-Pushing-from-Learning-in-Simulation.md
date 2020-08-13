---
layout: post
title: "Self-Adapting Recurrent Models for Object Pushing from Learning in Simulation"
date: 2020-08-12
---


[Lin Cong](https://tams.informatik.uni-hamburg.de/people/cong/), [Michael Görner](https://tams.informatik.uni-hamburg.de/people/goerner/), [Philipp Ruppel](https://tams.informatik.uni-hamburg.de/people/ruppel/), [Hongzhuo Liang](https://tams.informatik.uni-hamburg.de/people/liang/), [Norman Hendrich](https://tams.informatik.uni-hamburg.de/people/hendrich/), [Jianwei Zhang](https://tams.informatik.uni-hamburg.de/people/zhang/)

## Related works and why do we propose this model

Planar pushing problem has attracted many famous research groups' attention. Planar object pushing with a single contact is a typical under-actuated instance of robot manipulation. The uncertainty of different physics parameters and the pressure distribution makes it difficult to build a precise motion model for real interactions. Learning a data-driven model ([M.Bauza & A.Rodriguez](https://arxiv.org/abs/1704.03033)) is an effective method due to the stochastic nature of the pushing process. Valuable dataset including [Omnipush Dataset](http://web.mit.edu/mcube/omnipush-dataset/) by MIT, [Pushing Dataset](https://sites.google.com/site/brainrobotdata/home/push-dataset) by Google Brain are open to the whole community. Besides the model-based method, end-to-end policy learning by mapping from state space to action space directly is also becoming a trend.

Recurrent Neural Networks (RNNs) have long been used for fitting nonlinear dynamic models.
With the distinctive ability to recognize patterns in sequences of data, the LSTM module is chosen to fit the object motion dynamics during the pushing process. We use an LSTM-based model to predict the motion of objects with unknown parameters
and apply [Model Predictive Path Integral](https://homes.cs.washington.edu/~bboots/files/InformationTheoreticMPC.pdf) as control strategy to push the objects to target poses with a single point of contact.

![Planar pushing object motion prediction problem]({{ site.url }}/data/images/self-adapting-description.png)
{: style="width: 100%;" class="center"}
*Figure 1. The planar pushing object movement prediction problem*

## Recurrent Model

Humans can approximate dynamic models from several pushing steps during the interaction with an object and choose the suitable pushing direction and velocity given a target pose. Inspired by this memory learning process, we choose an LSTM module as the main part of our dynamic model.

![LSTM]({{ site.url }}/data/images/self-adapting-LSTM.png)
{: style="width: 100%;" class="center"}
*Figure 2. The recurrent model*

## Recurrent Model Predictive Path Integral

In order to endow the original [MPPI](https://homes.cs.washington.edu/~bboots/files/InformationTheoreticMPC.pdf) with a memory mechanism, we add a history buffer $\mathcal{H}$ into the algorithm. Algorithm 1 gives details of the whole framework. The results from our real experiments prove the effectiveness of RMPPI.

![Algorithm]({{ site.url }}/data/images/self-adapting-algorithm.png)
{: style="width: 100%;" class="center"}
*Figure 3. RMPPI*
