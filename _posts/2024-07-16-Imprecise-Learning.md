---
layout: post
title: "Imprecise Learning"
date: 2024-07-16
---
## A self-driving AI's dilemma
<p align="center">
<img src="https://anurag14.github.io/blog_resources/2024-07-17/thought.png" width="800" height="200" />
</p>
<p align ="center">
Fig1: A self driving car thought experiment
</p>
Consider a hypothetical scenario where a self-driving AI, trained on data from diverse countries and driving conditions, is deployed in various vehicles operating under different regulations. The question arises: should this AI make the same decision in identical situations across all these vehicles?

The AI needs to behave differently based on the type of vehicle. Private cars always carry passengers, whereas commercial vehicles typically carry payloads. In an accident scenario, the AI in a private car should prioritize saving the passenger, while in a commercial vehicle, the priority might be to protect humans outside the vehicle. Cabs need to behave like private cars, prioritizing passenger safety when occupied.

In real-world deployments, such context-dependent scenarios are common. Current machine learning models struggle to adapt because developers often "hard-code" generalization notions without sufficient context. These rules, or situation-dependent priorities, are user-specific and only become clear at deployment.

## Approach of Imprecise Learnering 
<p align="center">
<img src="https://anurag14.github.io/blog_resources/2024-07-17/tldr.png" width="800" height="200" />
</p>
<p align ="center">
Fig2: We train a bunch of models that the user can pick from at test time. 
</p>

Training machine learning models with fixed generalization notions often leads to alignment problems. Using a gifting analogy, buying a gift without knowing the recipient's preferences often results in a mismatched gift. Similarly, providing a fixed model without understanding user-specific needs leads to misalignment.

One possible solution is to give users the training data so they can train an aligned model themselves, akin to giving money instead of a gift. While this resolves the alignment issue, it imposes a burden on the user and raises privacy concerns.

We propose an alternative: the model developer trains a collection of models, allowing the user to choose the one that best aligns with their needs at test time. In the gifting analogy, this is like offering multiple gifts for the recipient to choose from. Although this approach is computationally more expensive, similar to buying multiple gifts, it balances alignment and privacy concerns without needing to release the training data.

## How does Imprecise Learning differ from standard learning frameworks?
<p align="center">
<img src="https://anurag14.github.io/blog_resources/2024-07-17/introduction.png" width="800" height="200" />
</p>
<p align ="center">
Fig3: How are assumptions on developers and users relaxed in the Imprecise Learning framework compared to previous settings. 
</p>

Generalization is a well-studied topic in machine learning, crucial for understanding the assumptions that ensure learning and how these assumptions play out in real-world scenarios. Broadly, generalization has been explored in two main settings: in-distribution (IID) generalization and out-of-distribution (OOD) generalization. IID settings assume that both training and deployment environments come from an unknown fixed distribution P. In contrast, OOD generalization relaxes this assumption, allowing for different distributions during training and deployment.

Under the IID assumption, developers know that the test-time distribution matches the training-time distribution, providing a clear understanding of the user's deployment situation. This allows the learner to optimize precisely for a single distribution. In OOD settings, where the test-time distribution is unknown, frameworks often optimize for the worst-case distribution, assuming this will cover most scenarios. This approach also represents a precise choice, committing to a specific distribution under uncertainty.

However, precise generalization notions can lead to misalignment due to arbitrary commitments to distributions under uncertainty. Imprecise learning, on the other hand, does not commit to a single distribution. Instead, developers consider a set of possible distributions, known as the credal set within the Imprecise Probability community. The credal set represents the set of rational beliefs or distributions that agents can be uncertain about. By acknowledging that developers cannot know all user scenarios and deployment conditions, imprecise learning trains models for various possible distributions within this set.

## Imprecise Learning in domain generalisation

To model the idea of being imprecise while learning we consider a domain generalisation task. Usually domain generalisation problem is a OOD problem where learners start with a bunch of domains ${1,\cdots,d}$. 
For each domain we can write a population risk, which requires 3 components 
- A Hypothesis class $F$
- A loss function $\ell$
- A unknown data generation distribution $P$

Then we have our population risk,  $$\mathcal{R}(f)=\mathbb{E}_{P}[\ell(f(x),y)]$$
Usually a model that minimises this risk is called Bayes-optimal $$f_{Bayes}=argmin_{f\in F}\mathcal{R}(f)$$

Now in practice when we have data from different domains we optimize a profile of risks coming from $d$ domains. Here the alignment task shows up in how we aggergate the risk profile to optimize.

<p align="center">
<img src="https://anurag14.github.io/blog_resources/2024-07-17/motivation.png" width="700" height="250"/>
</p>
<p align ="center">
Fig4: How choice of aggerating the risk profile introduces decision making into domain generalisation. 
</p>

## Components of Imprecise Learning framework

To allow users to make the decision of which notion of generalisation should the model follow, we need to create a choice space that will allow the users to interpret and influence the model behavior. We call this choice space $\Lambda$. 

### User behavior parameterized objectives 
Users choices should influence model behavior. To achieve this, we need to map the choice space to corresponding objectives. These corresponding objectives will make model exhibit user desired behaviour, when a model is trained using them. This is achevied by aggeration functions which transform our original risk profile into user behavior parameterized objectives.

<p align="center">
<img src="https://anurag14.github.io/blog_resources/2024-07-17/agg_cvar.png" width="800" height="200" />
</p>
<p align ="center">
Fig4: Aggregation functions allow us to get user behavior parameterized objectives and Conditional Value at Risk (CVaR) is a example of such aggregation. 
</p>

### Augmented Hypothesis
We need to also allow users to recover the model that agrees with their choice at test time, therefore the user's choice should also influcence the model. Therefore, we consider classes of models which depend on both the input and choice for giving output. 

<p align="center">
<img src="https://anurag14.github.io/blog_resources/2024-07-17/hypernetwork.png"  width="600" height="150" />
</p>
<p align ="center">
Fig5: Augmented Hypothesis models are user choice dependent. 
</p>

## How do we optimize to learn within such framework?

## Summary

##### Step 1: Developer represents their uncertainty with credal set
<p align="center">
<img src="https://anurag14.github.io/blog_resources/2024-07-17/step1.png" width="800" height="120" />
</p>

##### Step 2: Map credal set to user behaviour choice space $\Lambda$ and pick hypothesis class 
<p align="center">
<img src="https://anurag14.github.io/blog_resources/2024-07-17/step2.png" width="800" height="120" />
</p>

##### Step 3: Find a distribution that makes Pareto Improvement for model update
<p align="center">
<img src="https://anurag14.github.io/blog_resources/2024-07-17/step3.png" width="800" height="120" />
</p>

##### Step 4: At deployment users can consume model $h(\cdot,\lambda)$ with their choice of $\lambda\in\Lambda$