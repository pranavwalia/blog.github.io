---
layout: post
title: The St. Petersburg Paradox, When EV Isn't Enough
categories: [Game Theory, Mathematics]
tags: [Game Theory, Risk, Math]
fullview: false
usemathjax: true
comments: false
---
Today we will discuss a famous problem known as the St. Petersburg Paradox. The problem was originally presented by [Daniel Bernoulli](https://en.wikipedia.org/wiki/Daniel_Bernoulli) in 1738 in the Commentaries of the Imperial Academy of Science of Saint Petersburg (hence the name). The problem demonstrates that certain games may have extremely high payoff/utility yet the variance of outcomes can be such that no sensible person would participate (despite extremely high expectation).

### The Problem

Suppose you are paying a fixed fee to participate in a coin tossing game. Assume that the coin is evenly weighted (fair). The coin will be tossed repeatedly.

There is a cash prize that starts at 1$. Every time the coin lands heads, the size of the pot doubles. Once the coin lands of tails, the game ends and you win whatever is contained in the pot.

How much should you pay to play this game in order to break even?

### Expected Value of The Game

Well from basic decision theory we know that a break-even decision is one where the cost is equal to the utility of a decision. Therefore, in order to calculate the break-even price, we simply need to calculate the expected value of the game.

We know that the probability of flipping n heads consecutively is

$$
\frac{1}{2^n}
$$

Since we win $1 if the first flip is tails (0 heads), the payoff on the nth consecutive head is

$$
2^{n -1}
$$

So for a single value of n, where n is the number of consecutive heads we get in a single session of the game, the expectation would be

$$
\frac{1}{2^n} * 2^{n -1}
$$

​	Are we done? NO! A single value of n only measures one branch of the game tree. But there are an infinite number of branches on the game tree. The higher n is, the lower the probability of that specific outcome on the game tree, yet there is an outcome for every possible branch. Therefore, the entire expectation can be represented by an infinite sum.

$$
\sum_{n=1}^{\infty} \frac{1}{2^n} * 2^{n -1} = \infty
$$

We can see that the infinite sum converges to infinity! Don't believe me? Let's step through the sum for each value of n.

$$
E[\infty] = (\frac{1}{2} * 1) + (\frac{1}{4} * 2) + (\frac{1}{8} * 4)...
$$

We can see that if we continue we will get an infinite sum of 1/2's. Therefore, the expectation of the game is infinity! So hypothetically, the break-even price to play this game is also infinity. 



### Where's The Paradox?

The paradox is that despite the game having such a high payoff, nobody with common sense would pay more than a few dollars to play the game. This is because the branches of the game tree with high payoffs are extremely hard to reach, yet since the utility of those branches grow at a similar rate, the expectation does not diminish for lower probability events as it would in most games.
