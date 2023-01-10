---
layout: page
title: Preference-based Reinforcement Learning
description: Preferences are relative human evaluation for agent behaviors. This project aims at training RL agents using human evaluation and enables agents to learn from humans.
img: assets/img/pbrl/system_diagram.png
importance: 1
category: Research
---

## Motivation

Suppose an agent just played a game in front of you. Even though you are not an expert for the game, you probably can get some sense about how well it played, based on clues such as if it lost a life or game scores. In other word, sometimes we humans can evaluate how well an agent performs based on common knowledge.

In the meantime, a common challenge for reinforcement learning (RL) application is the lack of reward, which is a function that evaluats agent behaviors. Take the real-time strategic game Starcraft II as an example. In a game an agent makes thousands of decisions, but strictly speaking it only receives one direct feedback at the end of game—win or loss. Moreover, there are tasks that do not have pre-defined rewards. For example, the goal of home robots is to assist individual users, so it is essential for them to adapt to individual users. However, this is only possible after a robot is brought to ones' home; it is impossible to have access to individual users' needs beforehand.

To address the abovementioned challenge, this project aims at training RL agents using human-generated evaluations and enables agents to learn from humans. In particular, this projects considers preferences as the form of human evaluation. Roughly, a preference specifies the one from a pair of behaviors that is more preferable. Consider the following example.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/pbrl/ant_good.webp" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/pbrl/ant_bad.webp" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    An example for preferences, which are videos for an agent controling ant-like robot. In this example the left one if better, as in the right video the agent's robot fell over.
</div>

One nice thing about preferences is that it require less expertise than other types of feedbacks. Annotators are not required to quantify the optimality of agents' behaviors; they only needs to provide relative comparisons. In fact, both videos in the example above are not optimal; in the left video the agent raised one of the robot's leg to a position that might cause instability. Yet annotators do not have to consider such details when giving preferences, as falling over is an eye-catching failure.  




## Research Questions

**How to develop agents using noisy preferences?**

Preference collection can be an issue in practice. Existing studies recruit collaborators for preference generation, which is limited by the availability of collaborators and expansive. This work overcomed such drawback by developing an algorithm to learn reward functions from noisy preferences, which enables one to collect low-priced preferences via crowdsourcing.

A conference paper for this work is accepted by ECML-PKDD 2022. A video overview is provided below, and you are also welcome to read the [poster]({{ relative_url }}/assets/pdf/batch_reinforcement_learning_from_crowds_poster.pdf) and the [paper](https://arxiv.org/abs/2111.04279).
{% include youtubePlayer.html width="640" height="360" id="npJzZzaEDCA" %}
<br/>

**How to systematically interpret the learned reward functions?**

As in preference-based RL agents are supposed to learn from humans and probably work with humans, interpretability becomes a first principle. To develop trust between human and agents, it is of interest to reveal what kind of knowledge do agents acquire. Techniques for explainable AI usually construct explanations using data samples, yet there lacks a systematic approach to select samples for such purpose. As ad-hoc sample selection undermines the credibility of explanations, this work proposed an algorithm for inferring the importance of states during learning from preferences, which allows for examines the learned models using critical samples. See the below example for state importance.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/pbrl/identify_critical_states.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    An example for state importance. Left: a heatmap for state importance. Each row corresponds to a sequence of states, and the colors denote state importance. Upper right: an example for states with large absolute weights. The agent was closed to an incoming missile (circled in green) in the presence of enemies (circled in blue). Middle right: an example for states with weights close to zero. The agent launched missiles (circled in yellow) in open space. Bottom right: an example for transitioning from states with large absolute weights to states with small absolute weights, in which the agent lost a life (circled in red).
</div>

A journal paper for this work is accepted by *Machine Learning*, and a video overview is provided below. You are welcome to the [poster]({{ relative_url }}/assets/pdf/learning_state_importance_for_preference_based_reinforcement_learning_poster.pdf) and the [paper](https://rdcu.be/c245z). This [website](http://guoxizhang.com/identify-critical-states/) contains a categorization of inferred critical states that showcase the efficacy of this algorithm.
{% include youtubePlayer.html width="640" height="360" id="t7x1FmKrMyw" %}