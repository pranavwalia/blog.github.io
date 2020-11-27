---
layout: post
title: Basic Counterfactual Regret Minimization (Rock Paper Scissors)
description: In this article we will introduce an important concept of algorithmic game theory through the basic example of rock paper scissors.
categories: [Computer Science, Algorithms, Game Theory]
tags: [Counterfactual Regret Minimization, Algorithms, Game Theory, Computer Science, Algorithmic Game Theory]
permalink: CFRM-RPS
fullview: false
usemathjax: true
comments: false
---

![AI](/assets/images/ai.jpg) 

# Counterfactual Regret Minimization (Rock Paper Scissors)

Counterfactual regret minimization is an important concept in algorithmic game theory. It has made the creation of super-human poker AI possible and is fundamental for solving games of imperfect information. Today we will be implementing a rock paper scissors solver. Rock paper scissors is a useful introductory example as the game has a trivial solution (just play each option 33.333% of the time randomly). Solving rock paper scissors will lay the groundwork for solving more complex games (which we will do in future articles). 

**Note: All Code Implemented In Python**

### High Level Overview:

The algorithm will start with a hard-coded default strategy profile. At every iteration, the solver will compute a 'regret matched' strategy. This is a strategy that makes the minimum viable adjustment according to the observed result. This adjusted result is then added to a running sum of all previous adjustments. The resulting *game theory optimal* strategy will be the average of all adjusted strategies (sum of the strategies divided by the number of iterations).

**For Some Number of Iterations:**

   * Compute a regret-matching strategy
   * Add strategy profile to the profile sum
   * Select each player action profile according to the strategy profile
   * Compute regrets
   * Add player regrets to player cumulative regrets
   * Return the average strategy profile

## Rock Paper Scissors

To solve rock paper scissors we will need to program our agent to keep track of it's current strategy and update it iteratively. There are 2 variables that are key to the algorithm. The regret sum, and the strategy sum. The regret sum is an array that records all the lost utility by choosing the suboptimal decision in the moment. The strategy sum is the sum of all adjusted strategies.

### Key Variables:

* Indices to access options in strategy list
* regretSum: A list to keep track of the total regret of each decision
* strategy: A list to hold the weightings of each option in a mixed strategy
* strategySum: The sum of all the strategies used thus far
* oppStrategy: The strategy of a theoretical opponent against whom we must adjust


```python
import random
```

### Regret Matching
 * Computes the strategy as the accumulated regrets / total regret
 * Computes the strategy sum as the given strategy sum + the newly derived strategy based on accumulated regrets


```python
##Returns the adjusted strategy after an iteration
def getStrategy(regretSum,strategySum):
    actions = 3
    normalizingSum = 0
    strategy = [0,0,0]
    #Normalizingsum is the sum of positive regrets. 
    #This ensures do not 'over-adjust' and converge to equilibrium
    for i in range(0,actions):
        if regretSum[i] > 0:
            strategy[i] = regretSum[i]
        else:
            strategy[i] = 0
        normalizingSum += strategy[i]
    ##This loop normalizes our updated strategy
    for i in range(0,actions):
        if normalizingSum > 0:
            strategy[i] = strategy[i]/normalizingSum
        else:
            #Default to 33%
            strategy[i] = 1.0 / actions
        strategySum[i] += strategy[i]
    return (strategy,strategySum)
```

### Pull A Random Action According To Current Mixed Strategy

This function will choose a random action based on our most updated strategy. Remember that the strategy list stores all the weightings for each action.


```python
#Returns a random action according to the strategy
def getAction(strategy):
    r = random.uniform(0,1)
    if r >= 0 and r < strategy[0]:
        return 0
    elif r >= strategy[0] and r < strategy[0] + strategy[1]:
        return 1
    elif r >= strategy[0] + strategy[1] and r < sum(strategy):
        return 2
    else:
        return 0
```

### Training Algorithm

The following algorithm will compute the *maximally exploitative strategy* vs a fixed strategy from an opponent. For rock paper scissors, the nash equilibrium strategy dictates that any strategy which performs an action more than 33% dictates that we play the opposing action 100% of the time.

#### Maximally Exploitative Strategy Example:

Let us say our opponent is playing the following strategy:

- Rock: 34% 
- Paper: 33%
- Scissors: 33%

Knowing our opponent's strategy, we can compute the utility of each option


$$
EV(Rock) = .34(0) + .33(-1) + .33(1) = 0
$$


The expected value of choosing rock is zero since it ties 34% of the time, loses 33% of the time and wins another 33% of the time.


$$
EV(Scissors) = .34(-1) + .33(1) + .33(0) = -.01
$$


The expected value of choosing scissors is -.01 since it loses to rock 34% of the time, wins against paper 33% of the time, and ties to scissors 33% of the time.


$$
EV(Paper) = .34(1) + .33(0) + .33(-1) = .01
$$


The expected value of choosing paper is .01 since we win against rock 34% of the time, ties paper 33% of the time, and loses to scissors 33% of the time.

Knowing that the expected value of choosing paper is higher than any other option, the maximally exploitative strategy would be to always play paper.

#### Maximally Exploitative Function

The algorithm for training our agent to learn the maximally exploitative strategy can be described as follows.

- Accumulate regretSums after every round
- Compute a regret-matching strategy based on those regret sums
- Add Strategy to the sum of all the previously computed profiles


```python
def train(iterations,regretSum,oppStrategy):
    actionUtility = [0,0,0]
    strategySum = [0,0,0]
    actions = 3
    for i in range(0,iterations):
        ##Retrieve Actions
        t = getStrategy(regretSum,strategySum)
        strategy = t[0]
        strategySum = t[1]
        #print(strategy)
        myaction = getAction(strategy)
        #Define an arbitrary opponent strategy from which to adjust
        otherAction = getAction(oppStrategy)   
        #Opponent Chooses scissors
        if otherAction == actions - 1:
            #Utility(Rock) = 1
            actionUtility[0] = 1
            #Utility(Paper) = -1
            actionUtility[1] = -1
        #Opponent Chooses Rock
        elif otherAction == 0:
            #Utility(Scissors) = -1
            actionUtility[actions - 1] = -1
            #Utility(Paper) = 1
            actionUtility[1] = 1
        #Opopnent Chooses Paper
        else:
            #Utility(Rock) = -1
            actionUtility[0] = -1
            #Utility(Scissors) = 1
            actionUtility[2] = 1
            
        #Add the regrets from this decision
        for i in range(0,actions):
            regretSum[i] += actionUtility[i] - actionUtility[myaction]
    return strategySum
        
```

### Compute the average strategy
- Returns the average strategy profile as each option divided by the total sum of all options


```python
def getAverageStrategy(iterations,oppStrategy):
    actions = 3
    strategySum = train(iterations,[0,0,0],oppStrategy)
    avgStrategy = [0,0,0]
    normalizingSum = 0
    for i in range(0,actions):
        normalizingSum += strategySum[i]
    for i in range(0,actions):
        if normalizingSum > 0:
            avgStrategy[i] = strategySum[i] / normalizingSum
        else:
            avgStrategy[i] = 1.0 / actions
    return avgStrategy
```

### Run the algorithm!
* Demonstrates that we can generate a maximally exploitative strat


```python
oppStrat = [.4,.3,.3]
print("Opponent's Strategy",oppStrat)
print("Maximally Exploitative Strat", getAverageStrategy(1000000,oppStrat))
```

    Opponent's Strategy [0.4, 0.3, 0.3]
    Maximally Exploitative Strat [6.666666666666666e-07, 0.999999, 3.333333333333333e-07]


### Have Both Agents Converge to Nash Equilibrium
   * We will adapt our training algorithm to train two agents simultaneously


```python
#Two player training Function
def train2Player(iterations,regretSum1,regretSum2,p2Strat):
    ##Adapt Train Function for two players
    actions = 3
    actionUtility = [0,0,0]
    strategySum1 = [0,0,0]
    strategySum2 = [0,0,0]
    for i in range(0,iterations):
        ##Retrieve Actions
        t1 = getStrategy(regretSum1,strategySum1)
        strategy1 = t1[0]
        strategySum1 = t1[1]
        myaction = getAction(strategy1)
        t2 = getStrategy(regretSum2,p2Strat)
        strategy2 = t2[0]
        strategySum2 = t2[1]
        otherAction = getAction(strategy2)
        
        #Opponent Chooses scissors
        if otherAction == actions - 1:
            #Utility(Rock) = 1
            actionUtility[0] = 1
            #Utility(Paper) = -1
            actionUtility[1] = -1
        #Opponent Chooses Rock
        elif otherAction == 0:
            #Utility(Scissors) = -1
            actionUtility[actions - 1] = -1
            #Utility(Paper) = 1
            actionUtility[1] = 1
        #Opopnent Chooses Paper
        else:
            #Utility(Rock) = -1
            actionUtility[0] = -1
            #Utility(Scissors) = 1
            actionUtility[2] = 1
            
        #Add the regrets from this decision
        for i in range(0,actions):
            regretSum1[i] += actionUtility[i] - actionUtility[myaction]
            regretSum2[i] += -(actionUtility[i] - actionUtility[myaction])
    return (strategySum1, strategySum2)

#Returns a nash equilibrium reached by two opponents through CFRM
def RPStoNash(iterations,oppStrat):
    strats = train2Player(iterations,[0,0,0],[0,0,0],oppStrat)
    s1 = sum(strats[0])
    s2 = sum(strats[1])
    for i in range(3):
        if s1 > 0:
            strats[0][i] = strats[0][i]/s1
        if s2 > 0:
            strats[1][i] = strats[1][i]/s2
    return strats

```


```python
print(RPStoNash(1000000,[.4,.3,.3]))
```

    Player 1                                                     Player 2
    ([0.34083239238186, 0.3340920629119219, 0.3250755447062181], [0.32967926313477963, 0.33222032740623947, 0.3381004094589809])
As we can see. The final strategy is around 33% for all options for each player.


