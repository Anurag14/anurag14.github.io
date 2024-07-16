---
layout: post
title: "Imprecise Learning"
date: 2024-07-16
---
## A self-driving AI's dilemma
<p align="center">
<img src="https://anurag14.github.io/blog_resources/2024-07-17/thought-1.png" width="400" height="200" />
</p>
<p align ="center">
Fig1: A self driving car thought experiment
</p>
Let's consider a hypothetical scenario. When a self driving AI company creates a self-driving AI that is trained on data from diverse countries and driving scenarios. It will then be deployed in different vehicles operating in different regulations and conditions. 

The question then is, should this AI take same decision in same situation in all these vehicles? If we ponder, we will realise that the AI model needs to behave differently in each vehicle. Private cars always carry a passenger, whereas commerical vehicles will only carry payloads. Then the action that model needs to take in an accident situation, will depend on the vehicle. AI model in an private car needs to priortise to save human inside the car and in case of carrying payloads humans outside the vehicle take priority. Cabs need to behave like private cars and liek 


In the real world, such situations always occur at the time of deployment. Our current machine learning models fail to adapt to these scenarios because model developers "hard-code" the notions of generalisation without their lack of knowledge about them. This notion of generalisation or equivalently situation dependent priorities that affect the decisions are essentially user choices and thus only known concretely at the deployment time.  

With imprecise learning our aim is to develop better generalisation frameworks which lead us closer to machine learning models that work desirably in real world sitautions similar to our thought experiment. 

## Approach of Imprecise Learnering 
<p align="center">
<img src="https://anurag14.github.io/blog_resources/2024-07-17/tldr.png" width="400" height="200" />
</p>
<p align ="center">
Fig2: We train a bunch of models that the user can pick from at test time. 
</p>

Given we want to train machine learning models such that users suitable to consume according to their notion of generalisation giving a fixed model is definitely going to lead an alignment problem. In a gifting analogy, buying a gift without knowledge of what our receivers want always comes with the issues of gift not meeting receiver's preferences. Then what is the solution ? Should we just give the training data to our user and let them train an aligned model? Just like giving money to receiver so that they can buy the gift they want. This will solve the alignment issue but induces work on user side, and often is also not a feasible solution due to privacy concerns. 

We propose that the model developer trains a bunch of models and then let the user pick the model that aligns to their needs at test time. In gifting analogy, this stands for having multiple gifts from which receiver can pick the gift that they want. There are some obvious limitations to this approach that buying multiple gifts is costlier than a single gift thus this approach is computationally more expensive but it allows us to get the best of both worlds where we can solve for alignment problem and also need not release the data. 

## How does Imprecise Learning differ from standard learning frameworks?
<p align="center">
<img src="https://anurag14.github.io/blog_resources/2024-07-17/introduction.png" width="400" height="200" />
</p>
<p align ="center">
Fig3: How are assumptions on developers and users relaxed in the Imprecise Learning framework compared to previous settings. 
</p>

Generalisation has been one of the most well studied topics in machine learning. It is super important to understand the assumptions under which prior works have guaranteed learning and how those assumptions play out in the real world. Broadly speaking, generalisation has been studied in majorly two settings, in-distribution (IID) generalisation and out-of-distribution (OOD) generalisation. IID settings assume that both their training and deployment enviroments come from an unknown fixed distribution $P$. Whereas in out-of-distribution (OOD) generalisation we relax this assumption that training and deployment environments come from the same distribution. 

With the IID assumption developer knows that the test time distribution is going to be same as training time, in some sense we know the users delopyment situation completely. Therefore learner commits to a single distribution over which it can learn from the different choice of distributions a learner can assume to perform optimisation, we call this as being **_Precise_**. With the relaxation of IID assumption in the OOD settings the most of the frameworks now are unaware of which distribution they will encounter at the test time, however they arbitrarily pick the worst case distribution to optimise for, assuming the worst case optimisation will allow them to work in most of the scenarios. This choice of arbitrarily commiting to a worse case distribution under uncertainty also is a precise choice. Thus, all current learning frameworks follow a precise generalisation notion to obtain a model. 

This preicse generalisation notion due to commiting arbitrarily to a distribution under uncertainty causes misalignment. On the contrary in **_Imprecise_** setting a developer does not commit to a single distribution to train model on but rather trains models for every possible scenario of distributions since they don't know who their user will be and in what situations will they use their model. Okay, not every possible scenario but the developer starts with a set of possible scenario of distributions and then trains model of every distribution in that set. Within Imprecise Probability community this set is called as the credal set. Credals sets represent the set of rational beliefs / distributions that the agents can be uncertain about. Acknowledging that learners don't know who their user will be is important, going back to our thought experiment there is no way for the self driving AI developers to know a fixed model output for a data input since the right decision also depends on situations (eg. type of vehicle) which are only known at test-time. 

## Imprecise Learning in action

To model the idea of being imprecise while learning we consider a domain generalisation task. Usually domain generalisation problem is a OOD problem where learners start with a bunch of domains ${1,\cdots,d}$. 
> For each domain we can write a population risk, which requires 3 components 
> - A Hypothesis class $F$
> - A loss function $\ell$
> - A unknown data generation distribution $P$

Then we have our risk, usually a model that minimises this risk is called Bayes-optimal
> $$\mathcal{R}=\mathbb{E}_{P}[\ell(f(x),y)]$$ 