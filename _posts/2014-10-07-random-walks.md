---
layout      : post
title       : A Philosophical Study of Random Walks
subtitle    : Understanding Intuition vs Probability, Choices in time
author      : Naveen Venkataraman
comments    : True
permalink   : random-walks
---

I've been taking a class in Statistical Analysis with Prof. [Yuri Balasanov](http://www-finmath.uchicago.edu/about/faculty.shtml#balasanov) and we recently covered the concept of a [Random Walk](http://en.wikipedia.org/wiki/Random_walk).

Random Walks are interesting to study because they expose the frailty of our grasp over probabilistic thinking. They are also interesting from a philosophical point of view. A minor class discussion point moved me immensely and inspired me to write this post to illustrate the power of choices.

---

##### What is a Random Walk?

In very simple layman's terms, a random walk is a succession of random steps with a probability associated with each outcome. This is typically illustrated using a (fair) coin toss.

Let's illustrate these points and test our intuition using using a fair coin i.e a coin whose probability of Heads = probability of Tails = 0.5.

---

##### Expt 1: If I flipped the coin 100,000 times, what probability will the tails converge at?

If you guessed 0.5, you're right! As the graph below shows, over a large enough sample, the convergence is at 0.5.

__Graph 1: Convergence of tails__
<img src="https://cloud.githubusercontent.com/assets/2165419/4553104/495ef806-4e93-11e4-96c2-92c231278ad3.png"/>

So far, so good.

---

##### Expt 2: Let's play a game. I give you a dollar each time the coin lands as a tail and take away a dollar each time the coin lands as heads. If we flipped the coin a million times, how much money do you think you will make?

Given the results of the first experiment, most people would guess that the profits and losses would net themselves out and we would end up with a zero profit.

__Graph 2: Random Walks__
<img src="https://cloud.githubusercontent.com/assets/2165419/4554155/35dd6032-4ea8-11e4-9903-9273156748f5.png"/>

But in reality, there are several possibilities as illustrated by the graph that follows. This is the core illustration of a Random Walk, and this is the point at which I had a mini "Aha!" moment.

These basic set of graphs illustrate two fundamentally simple, yet profound points:

1. A random walk is not mean converging. In simple English: While the probability of an individual event may be 50-50, a cumulative outcome will vary significantly from the expected average outcome. This has significant implications in financial markets, but also in day to day activities such as individual performances, individual choices etc.

2. The graphs demonstrate possible outcomes from time t = 0 to t = INF. Some graphs consistently go up, others go down while yet others oscillate. Any time an individual plays this game, s/he is already pinned to a single path of outcomes. However, and this was my fundamental insight, at any time t = N, an individual **ALWAYS HAS A CHOICE** _to play or not to play_.

__Graph 3: Illustration of Choice__
<img src="https://cloud.githubusercontent.com/assets/2165419/4554353/b05a9358-4eac-11e4-8143-b3e9bed01fc3.png"/>

This is because at any time t = N, though there are several paths and whilst an outcome cannot deviate from an individual path, the player always has a choice to play for the next outcome or to not play. This has the impact of changing the player's path from the one he is on to one he invents anew through choice and an equiprobable outcome. Basically, a player cannot switch paths, but can invent a new path for himself.

From a philosophical standpoint, I wonder if this is what we call destiny.