---
layout: post
title: Poker Theory Fundamentals
categories: [Poker Strategy, Game Theory]
tags: [Poker Strategy]
permalink: poker-theory-fundamentals
fullview: false
usemathjax: true
comments: false
---
In this article I will lay out the foundational knowledge required to begin learning modern GTO (Game Theory Optimal) poker. At this point, the GTO vs Exploitative debate has essentially been settled and most reasonable people have acknowledged that if you want to be a profitable poker player you need to have a solid understanding of theory. Any exploitation should generally occur as a deliberate deviation from what you understand to be a theoretically correct play. But, if you do not have a foundational understanding of what theoretically correct play even is, your exploitative plays will be based on accurate hunches (at best) and complete delusion (at worst). 

### Mathematical Foundations

Before diving into the foundations of GTO we will cover some very basic poker math. These concepts have been discussed ad nauseam in a variety of poker books but are still wroth being briefly mentioned.

#### Hand Combinatorics
There are three categories of hands:  
* Suited holdings
  * 4 combos per holding
  * eg. AKs - 4 combos, one of spades, clubs, diamonds, hearts
* Unsuited Holdings
  * 12 combos per holding
  * eg. AKo - 12 combos
* Pocket Pairs
  * 6 combos per holding
  * eg. 66 - 6 combos

#### Pocket Pair Combinatorics
**Pocket pairs** have six combos. So for the holding '66' there would be be:  

* 6 hearts 6 diamonds
* 6 hearts 6 spades
* 6 hearts 6 clubs
* 6 diamonds 6 clubs
* 6 diamonds 6 spades
* 6 spades 6 clubs 

Removing just one 6 from the deck takes the amount of possible combos to 3.
Removing another 6 from the deck brings the possible combos of 6 down to one.
(Check for yourself by trying to exclude a suit and see how many are left.

**Suited holdings** have 4 combos. Let's say we have AKs, removing the ace of hearts would take the number of combos down to 3. Removing  the king of hearts would have no effect since the AhKh combo has already been removed. Thus, the number of a suited combos in an opponent's range is easy to calculate.

**Off-suit Holdings** have 12 combos. The removal factor on off-suit holdings is slightly more nuanced. Take the example of AKo

AKo - 12 combos

Each Ace is mapped to exactly three king cards (every suit of king other than it's own suit). Likewise, each King is mapped to exactly three Ace cards.

Removing an Ace from the deck will make the possible number of AKo combos 9. Removing an King subsequently will take the number of combos down to 6. 

#### Outs and Equity:

The amount of outs a hand has is simply the number of possible cards left in the deck that can result in a player making a draw of a pair etc.

A common mental math calculation is to multiply the number of outs by 4 on the flop for the probability of making a hand such as a flop or a straight by the river and to multiply by 2 on the turn.

| Hand Type                | Outs |
| ------------------------ | ---- |
| Flush Draw               | 9    |
| Open Ended Straight Draw | 8    |
| Gut-shot Straight draw   | 4    |

#### Pot Odds:

When an opponent bets, pot odds can be calculated as  

$$
\frac{bet}{pot + bet}
$$

This will give you the frequency at which you would need to call to theoretically keep your opponent indifferent to bluffing you with any two cards (more on this later). But as we will later discover this approach to defense in the game is heavily outdated, however for players who are vastly under or over-defending vs raises and bets, this concept can be helpful. 

#### Hand Odds:

This will give you the amount of equity against your opponent's range required to defend against a bet. Again, this model is outdated and has been disproven by solvers but is still useful for beginners.

$$
\frac{bet}{2*bet + pot}
$$


### Range Morphology

A range is a set of hands. Preflop, you have a range for each action, whether you open-raise, 3-bet or flat an open defines that range. You range will interact with flops in a variety of ways. There are a few words we use to describe ranges and their states.

* Linear Range: A range that contains the best hands, the worst hands, and everything in-between
* Condensed Range: A range that is condensed contains mostly medium strength hands with very few if any strong and weak hands
* Polarized: A polarized range contains the strong hands and weak hands but very few if any medium strength hands
* Capped Range: A capped range is a range that does not contain the very strongest hands on a board runout
* Uncapped: An uncapped range contains the best possible holdings

 

### Basic Game Theory Optimal Concepts

Now that I have given you a brief summary of the foundations of poker strategy we will now dive into the basics of game theory optimal play. 

#### History of GTO Play

The idea of an optimal strategy to poker is as old as the field of game theory itself. Von Neumann cited poker as the inspiration of his early works on game theory and wanted to formalize the strategies behind bluffing. John Nash, and Harold W. Kuhn also developed poker toy games which they solved to equilibrium in order to further develop their ideas on games of hidden information.

#### Why Things Are Different Now

The old way of conducting game theory research was to come up with a game, formalize the rules, and attempt to calculate an equilibrium and utility payoff structure. After deeply analyzing the game tree, mathematicians could calculate optimal solutions either by hand or with some form of computational assistance.

This was the technique used by Edward O. Thorpe when he first invented card counting for blackjack. Now, with very fast computers, we can simply run simulations of model poker games and observe their solutions.

Rather than theorizing about what might be optimal play, we can simply observe optimal play and work backwards in terms of developing heuristics to imitate software.

#### GTO Concept 1: Minimum Defense Frequency

In around 2013, Matthew Janda published his widely acclaimed book "Applications of No-Limit Hold'em." This work popularized the concept of minimum defense frequencies and formed the back-bone of success behind many successful poker players such as Doug Polk, Ryan Fee and others. 

Yet, the concept of MDF was not anywhere close to being representative of actual GTO play. It was however, so vastly superior to whatever techniques others were using in their calling/raising strategies at the time, that it made a great many players rich beyond their wildest dreams.

Let us suppose that you are facing a bet on the river. Your hand consists of a medium strength bluff catcher, where your opponent either holds the nuts, or total air. In other words; your opponent has a 'perfectly polarized range' consisting of hands with either 100% equity or 0% equity at an even distribution vs your bluff catcher.

How would be go about calculating the optimal frequency at which you need to call in order to keep villain indifferent to bluffing? In other words, how can we call in such a way that the EV of betting is effectively zero, and villain gains no additional value by bluffing?

$$
EV[Bluffing] = 0 = (Pot)*(1 - C) - (Bet)*C
$$

When villain attempts to bluff us and we fold, he wins whatever is in the pot. When villain attempts to bluff us and we call, he loses whatever it is that he has bet.
By solving for the appropriate calling frequency we arrive at the conclusion that:

$$
C = \frac{Pot}{Pot + Bet}
$$

The idea is that by calling at least C% of the time, we can assure that our opponent will not gain any additional utility by betting with a hand that would lose at showdown.

#### GTO Concept 2: Value to Bluff Ratios

* Let there be two players, an IP (in position) and an OOP (out of position) player.
* Let IP have a perfectly polarized range on the river (hands with either 100% equity or 0% equity) so that whenever OOP calls we effectively win.

Question: What proportion of our river betting range should be value hands (hands that win at showdown) vs what proportion should be bluffs to make the EV of our opponent calling zero?

* Let X be our bluffing frequency on a river bet
* Let P be the original size of the pot
* Let B be the size of our bet
* Assume EV of Calling - EV of Folding = 0 (Our opponent is indifferent to either actions)
* EV of Folding is always zero, therefore we need to only solve EV[Call]

Our opponent will win the size of the pot + our bet when he calls our bluffs and will lose the size of our bet when he calls our value bets.

$$
EV[Call] = 0 = (P + B)x - B(1 - x)
$$

Solving for x

$$
X = B/(P + 2B)
$$

Now using our equation we can determine the frequency at which we should be bluffing for any given bet size where B is a fraction of P.

* Pot Sized Bet (B = P): 33% bluffs
* 3/4 Sized Bet (B = .75P): 30% bluffs
* 1/2 Sized Bet (B = .5P): 25% bluffs
* 1/3 Sized Bet (B = .33P): 20% bluffs

Let's of course notice that the larger our bet-size the more bluff heavy our range is! To most players this seems counter-intuitive but let's use some very simple reasoning to think through it. 

When an opponent calls our value bet, we win what's already in the pot + whatever we risked. When an opponent calls our bluff, we only lose what we risked. Larger bet sizes cause a rational opponent to fold at a higher frequency meaning that we must accordingly add more bluffs.  Additionally, we can afford to lose at showdown often when we bluff since value bets will win us much larger pots. Large bet sizes are positively correlated with a more polarized range (separation between bluffs and value bets) whereas smaller bet sizes are more useful when ranges are too heavy to want to generate folds. This is evident in many solver simulations.

### Conclusion

In this article we covered the bare bones fundamentals of poker. If you are a new player I hope you enjoyed this introduction. In future posts, we will dive deeper into solver based poker strategies!


