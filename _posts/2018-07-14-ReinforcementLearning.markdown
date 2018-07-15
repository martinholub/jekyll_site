---
layout: post
mathjax: true
title: Reinforcement Learning, Teaching AI to Play
date: 2018-07-14 10:42
tags: ETH projects code
categories: ETH code
description: |
    In this post, I will demonstrate and explain reinforcement learning code I developed. You will learn how one can train an AI agent to master Atari games and understand the technology behind DeepMind's AlphaGo, the first computer program to defeat professional human Go player.
---

<div class="img_row" style="width: 90%;">
  <img class="col three" src="/img/rl/breakout_head.jpg" alt="" title="Header" />
</div>

In this post, I will demonstrate and explain [Reinforcement Learning](https://en.wikipedia.org/wiki/Reinforcement_learning) code I developed. You will learn how one can train an AI agent to master Atari games and understand the technology behind [DeepMind's AlphaGo](https://deepmind.com/research/alphago/), the first computer program to defeat professional human Go player. This will be fun and, surprisingly, simple, so let's dive in.

## OpenAI Gym

[OpenAI's `gym`](https://github.com/openai/gym) is a toolkit for developing and comparing reinforcement learning algorithms. [Big standardized datasets](https://en.wikipedia.org/wiki/List_of_datasets_for_machine_learning_research) have proven pivotal in development of deep learning algorithms. Similarly, collection of test problems, environments, as provided by `gym` aids in evaluation of reinforcement learning algorithms when an agent learns to take actions in response to observations from environment to "solve it". All that comes below is enabled by the work of guys at OpenAI. Hat tip to them.

## The CartPole Problem

<div class="img_row" style = "width: 75%;">
  <img class="col three" src="{{ site.baseurl }}/img/rl/cartpole.gif" alt="" title="CartPole Agent"/>
</div>
<div class="col three caption">
Trained agent skillfully balancing the pole on the cart
</div>

The `CartPole-v0` environment is a reinforcement learning (RL) equivalent of *Hello World!*. As such, it is sufficiently simple to get us started. It is a form of the classic control problem of inverted pendulum where we balance a pole by moving a cart it is attached to either left or right. The environment is considered solved when the average reward is greater than or equal to 195.0 over 100 consecutive trials. You can check the environment's spec's at its [wiki](https://github.com/openai/gym/wiki/CartPole-v0).

### SARSA

To train an agent for this environment, I will use the [SARSA](https://en.wikipedia.org/wiki/State%E2%80%93action%E2%80%93reward%E2%80%93state%E2%80%93action) reinforcement learning algorithm. This is an *on-policy* learning algorithm (which means that it uses the same policy to generate both current $a_t$ as well as the next action $a_{t+1}$). The name SARSA comes from the fact that the update rule for a *Q-value* depends on the tuple $(s_t, a_t, r_t, s_{t+1}, a_{t+1})$, where $s_t$, $a_t$ and $r_t$ are state, action and reward at time $t$ respectively.

The concept of *Q-value* is simple one. You just need to understand that we need a value to optimize that describes the reward the agent has harvested during a period of gameplay. First, define *Value function* $V^{\pi}(s)$ which is an expected sum of discounted rewards upon starting at state $s$ and selecting actions according to policy $\pi$:

<!-- https://stats.stackexchange.com/questions/326788/when-to-choose-sarsa-vs-q-learning -->
<!-- https://datascience.stackexchange.com/questions/9832/what-is-the-q-function-and-what-is-the-v-function-in-reinforcement-learning/31791#31791 -->

$$
V^{\pi}(s) = E[R(s_0)+\gamma R(s_1)+\gamma^2 R(s_2) + ... | s_0=s,\pi].
$$

$R(\cdot)$ gives the immediate value of reward and the discount factor $\gamma$ expresses how much we care about past values of it. *Q-value* function is then just *V* function for a particular action $a_t$ for each state $s_t$. They are related with:

$$
V^\pi(s) = \sum_{a \in A} \pi (a|s)  * Q^\pi(a,s).
$$

Given the above definitions, the SARSA algorithm updates the *Q-value* by an error-term adjusted by the learning rate $\alpha$ as follows:

$$
Q(s_t,a_t)\leftarrow Q(s_t,a_t)+\alpha[r_{t+1}+\gamma Q(s_{t+1},a_{t+1})-Q(s_t,a_t)]
$$

In my implementation I [approximate](http://artint.info/2e/html/ArtInt2e.Ch12.S9.SS1.html) the *Q-values* for each action with a linear function and select an action with $argmax(w^Ts)$.

Here is the implementation (full code [here](https://gist.github.com/martinholub/c4860006d0cf3fbe87a79a054a9c98cd)):

{% gist c4860006d0cf3fbe87a79a054a9c98cd example.py %}

### Results

The algorithm works very well and we are able to solve the environment as early as after 60 or so episodes.

<div class="img_row" style = "width: 75%;">
  <img class="col three" src="{{ site.baseurl }}/img/rl/cartpole.png" alt="" title="Cartpole"/>
</div>
<div class="col three caption">
Solving the CartPole problem
</div>

## Atari Games

<div class="img_row" style = "width: 80%;">
  <img class="col three" src="{{ site.baseurl }}/img/rl/space_invaders.gif" alt="" title="SpaceInvaders"/>
</div>
<div class="col three caption">
Example of an Atari Game (Space Invaders)
</div>


After successfully training an agent on a simple problem, I jumped on something more complex. That is, teaching agent how to master *Atari games*. I focused on the game of [Breakout](https://gym.openai.com/envs/Breakout-v0/). This problem is very different from the previous one in that as input to our model we receive images of the game screen. Learning something from this complex input requires a model that is capable of abstracting features from it. This is why I decided to harness the power of a deep convolutional neural network.


### The Deep Model

For my implementation, I chose [the DQN model and algorithm](https://github.com/deepmind/dqn) that was used by DeepMind to learn how to play Go. I extended it by few recent developments from the field of deep reinforcement learning including the [dueling DQN](https://arxiv.org/pdf/1511.06581.pdf) and [double DQN](https://arxiv.org/pdf/1509.06461.pdf). I also used the [Prioritized Experience Replay Memory](https://github.com/rlcode/per) to train the agent on samples from past to prevent it forgetting about past experiences. The full code is available at [my GitHub](https://github.com/martinholub/demos-blogs-examples/tree/master/rl-gym/atari).

Here is the model in code:

{% gist 083d392d713e515fb5b96379a77670e0 model.py %}

You will see that the model architecture is pretty big. This is why the researchers at DeepMind had to train it for *50 million* frames to achieve great results. You will notice that I am using a [custom loss function](https://becominghuman.ai/beat-atari-with-deep-reinforcement-learning-part-2-dqn-improvements-d3563f665a2c). It allows me to update Q-values only for actions that were observed and also avoids the problem of weighting outliers too heavily that otherwise occurs with mean squared loss.

The [Huber loss](https://en.wikipedia.org/wiki/Huber_loss) is implemented as follows:

{% gist 083d392d713e515fb5b96379a77670e0 huber_loss.py %}

### Epsilon-Greedy Policy

I used `RMSProp` optimizer as it was also the one used in the original paper. Once the memory has been initialized with sufficient number of samples, then the network is retrained on each step by sampling a random batch from memory. The policy implemented is *Epsilon Greedy Policy* and it differs from the previously described SARSA algorithm in that it is implemented as an *off-policy* algorithm. That is, it chooses the next action in greedy fashion, in order to maximize the next reward.

{% gist 083d392d713e515fb5b96379a77670e0 training.py %}

### Checkpointing and Visualizations

Initially, I was getting hardly any improvements, even after many hours of training. I learned the hard way that ample and frequent checkpointing, logging and visualizations are absolute musts in training deep learning models. I found it the most convenient to define these with [Keras's `callbacks`](https://keras.io/callbacks/) and use [`TensorBoard`](https://www.tensorflow.org/guide/summaries_and_tensorboard) for monitoring them.  Here is an example of callbacks used to update mask of custom loss as well as to add custom visualization to TensorBoard.

{% gist 083d392d713e515fb5b96379a77670e0 callbacks_examples.py %}

For further examples of implementing callbacks in RL, check out the [keras-rl repo](https://github.com/keras-rl/keras-rl).


<div class="img_row">
  <img class="col three" src="{{ site.baseurl }}/img/rl/tensorboard.png" alt="" title="TensorBoard"/>
</div>
<div class="col three caption">
Example of TensorBoard visualizations showing progress on training (on x axis is number of frames).
</div>

### Results

After about 3000 episodes of training, my agent is able to play the game quite well :)

<div class="img_row" style = "width: 50%;">
  <img class="col three" src="{{ site.baseurl }}/img/rl/breakout.gif" alt="" title="BreakOut"/>
</div>
<div class="col three caption">
Independent AI agent playing BreakOut after 3000 episodes of training
</div>

## Conclusion

In this post, I have demonstrated that reinforcement learning problems can be solved with reasonably simple, yet very powerful algorithms, I also pin-pointed some critical aspects of training a DL/RL model. The reinforcement learning field has made great leaps forward in past years and it appears to be staying on this track. I am personally really excited about [applying RL in robotics](https://ai.googleblog.com/2018/06/scalable-deep-reinforcement-learning.html) and how will AI developed once it receives a physical body with means to experience and explore its environment.

*Thanks for reading, everyone!*

---

## Supplementary Info

### Takeaways

Below, I am listing some important personal takeaways. You will benefit from adopting them, especially if you didn't do much of a practical DL/RL previously.

* Make sure you can fit a tiny dataset/simple problem
* Before adopting and adapting reference implementation, test that it works
* Make changes incrementally and test that they produce expected results. First get something that works, only then make it nice.
* For RL, you don't need neither [BatchNormalization](https://keras.io/layers/normalization/) nor [Dropout](https://keras.io/layers/core/#dropout). Regularization is in general much less important than in other settings.
* Visualize loss, metrics, parameter updates, Q-values, actions and more throughout the training ([Callbacks]() and [Tensorboard]() are your friends)
* Periodically visualize the agent as it plays
* Get proper hardware for training. Either good desktop or remote resources.

I also created a [Reveal.js](https://github.com/hakimel/reveal.js) presentation where I go through these and other highly relevant and mainly practical aspects of deep learning models and training. <a href="{{ site.baseurl }}/data/dl-intro/index.html" target="_blank">Check it out here.</a>

### References

- [SARSA with Linear Function Approximation](http://artint.info/2e/html/ArtInt2e.Ch12.S9.SS1.html)
- [Value and Q-Value](https://datascience.stackexchange.com/questions/9832/what-is-the-q-function-and-what-is-the-v-function-in-reinforcement-learning/31791#31791)
- [Practical differneces between SARSA and Q-learning](https://stats.stackexchange.com/questions/326788/when-to-choose-sarsa-vs-q-learning)
