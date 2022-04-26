# Project 1: Google RecSim & SLATEQ
<p align="center">
AIPI 590 Final Project
</p>
<p align="center">
April 26th, 2022
</p>

<p align="center">
By Jasmine Young
</p>

### Introduction

Google RECSIM is a platform for users to author simulation environments that can be used with recommender systems. These environments are configurable and naturally support sequential interaction with users. The ability of RECSIM to reflect particular aspects of user behavior helps researchers to push the limits of current reinforcement learning. The environments can vary user preferences, item familiarity, user latent states, choice models, and other response behavior.

Many reinforcement learning recommender systems optimize their recommendations for long-term user engagement. However, in many cases users are presented with a slate of multiple items, and we need methods to deal with these unique situations in the reinforcement learning action space. SLATEQ is a decomposition of value-based temporal-difference and Q-learning that renders reinforcement learning tractable with slates. SLATEQ is able to maintain long term value by decomposing it into a function of its component item-wise long term values.

In this project I use Google RECSIM to build two environments. I then evaluate the performance of a SlateQ agent and a static agent in each environment. In this report I will explain the environments and agents that I used, the notebooks that make up my work, and the interesting results that I found.

### Methodology & Notebooks

##### I. Environments

There are multiple steps in creating the LTS environment in RECSIM. My intention was to re-create the Kale/Chocolate environment discussed in the Google RECSIM paper. The Kale/Chocolate environment assigns a degree of ‘kaleness’ to each item, representing the long term benefits of the item. Alternatively, the ‘chocolatey-ness’ of each item is equal to 1 - ‘kaleness’ and represents the short term enticement of the item. We begin by creating a document class and a document sampler so that each item is a document with a ‘kaleness’ value. Next we create a user state class, a user sampler, a user state transition model, and a user response model. Finally, our document sampler and user model come together into an LTS environment. 
The other environment I used is built in to RECSIM and represents the interest evolution of documents and users. The environment is called interest evolution and also has the capability of recommending slates of documents.

##### II. Agents

There are two agents I compare in this project - a SlateQ agent and a Static agent. The SlateQ agent implements full slate Q-Learning based on their DQN agent. This is a standard non-decomposed Q learning method that treats each slate as a single action. The other agent is a Static agent. The Static agent is built on RECSIM’s Abstract Episodic Recommender Agent. 

##### III. Notebook Table of Contents 

This table contains the list of notebooks present in my git repository and details their environment, agent type, slate size, and average episode rewards. In order to preserve RAM, I ran each environment/agent/slate size combination in a separate notebook. I was unable to run Notebook 7 and Notebook 15 without crashing due to lack of RAM, so I only present slate sizes 1-3 in the results.


<img width="630" alt="Screen Shot 2022-04-25 at 8 44 48 PM" src="https://user-images.githubusercontent.com/69827274/165197024-dcd00c95-c308-403e-8425-2006b38dc4cc.png">



### Results

The average episode rewards in the Kale/Chocolate environment are shown on the graph below. We see that the SlateQ agent performs better as the slate size increases. Alternatively, the static model performs worse as the slate size increases.




<img width="542" alt="Screen Shot 2022-04-25 at 8 47 10 PM" src="https://user-images.githubusercontent.com/69827274/165197144-6b3ad2e0-b504-4975-a68f-d3a30bb824f1.png">







The average episode rewards in the Interest Evolution environment are shown on the graph below. We see that the SlateQ agent performs better as the slate size increases, and by larger increments than in the Kale/Chocolate environment. We also note that the Static agent performs better as the slate size increases.



<img width="618" alt="Screen Shot 2022-04-25 at 8 47 20 PM" src="https://user-images.githubusercontent.com/69827274/165197161-154a9fc0-59b6-4c93-bf0d-e4aa8d4eefbf.png">



### Conclusions & Limitations

Overall, we see that in both environments, the SlateQ agent performs better as the slate size increases. However, the static agent only performed well with increasing slate size in the interest evolution environment. In the future this project could be improved by looking at larger slate sizes (4+). I was not able to do that here because of limited computational resources, but we would be able to see at what point the SlateQ agent begins to drop in performance. We could also explore variations in the design of the SlateQ agent.


