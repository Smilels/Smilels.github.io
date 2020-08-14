---
layout: post
title: "On going work, attention mechanism for reinforcement learning"
data: 2020-08-12
---

> This is an on going work. General idea is to highlight the important part which includes the necessary
information for the policy net. This is a pre-training stage or online training part which can be integrated into
a Reinforcement Learning framework. Here is some initial results, I will keep updating this blog.

# Initial Results of Attention Mechanism by Unsupervised Learning

Three columns from left to right are "original input", "attention map output" and "reconstruction output". The training process is shown:

1. On our UR5 platform, paying attention to the robot arm
![]({{ site.url }}/data/videos/attention-real-ur5-arm.gif)

2. On our UR5 platform, paying attention to the object
![]({{ site.url }}/data/videos/attention-real-ur5-object.gif)

3. On our simulation UR5 platform, paying attention to robot arm
![]({{ site.url }}/data/videos/attention-sim-ur5-arm.gif)

4. On [openai gym](https://gym.openai.com/), paying attention to robot arm
![]({{ site.url }}/data/videos/attention-fetch-arm.gif)

5. On [openai gym](https://gym.openai.com/), paying attention to object
![]({{ site.url }}/data/videos/attention-fetch-object.gif)

6. On [deep mind control tasks](https://deepmind.com/research/open-source/deepmind-control-suite)
![]({{ site.url }}/data/images/attention-cheetah.png)

![]({{ site.url }}/data/images/attention-cartpole.png)

![]({{ site.url }}/data/images/attention-fingerspin.png)

![]({{ site.url }}/data/images/attention-reach.png)

# Network deatails

To be continued :)
