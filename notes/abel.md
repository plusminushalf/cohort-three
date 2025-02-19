# Abel's notes
## Introduction
I'm a physicist, working on a PhD in genetics, and my excitement about formal treatments of complex systems has led me to Ethereum. 
More info is available at abeljansma.nl


## Updates

### [2022.10.24] First test with the `open-games-hs` engine
- Installed Haskell Tool Stack
- Forked the open game engine from [https://github.com/philipp-zahn/open-games-hs](https://github.com/philipp-zahn/open-games-hs)
- There was a bug in the Haskell tool stack that made `stack run` execute the wrong code. I submitted a PR to fix this [here](https://github.com/philipp-zahn/open-games-hs/pull/8).

In addition, I opened an interactive `ghci` session, and tested the simplest case: a single decision game where the optimum is choosing the number 5, with a squared error utility loss. This worked as it should:

```
λ: isOptimalSingleDecisionVerbose (pureIdentity 2)
----Analytics begin----
 Strategies are NOT in equilibrium. Consider the following profitable deviations:

Player: player1
Optimal Move: 5.0
Current Strategy: fromFreqs [(2.0,1.0)]
Optimal Payoff: 0.0
Current Payoff: -9.0
Observable State: ()
Unobservable State: "((),())"
 --other game--
 --No more information--
 NEWGAME:
----Analytics end----

λ: isOptimalSingleDecisionVerbose (pureIdentity 5)
----Analytics begin----
 Strategies are in equilibrium
 NEWGAME:
----Analytics end----
```

As a sanity check, changing the payoff function to the constant 0-function by setting `payoffFunction peak dec = - 0*(peak - dec)**2` in `Decision.hs` results in every strategy being an equilibrium:

```
λ: isOptimalSingleDecisionVerbose (pureIdentity 5)
----Analytics begin----
 Strategies are in equilibrium
 NEWGAME:
----Analytics end----

λ: isOptimalSingleDecisionVerbose (pureIdentity 2)
----Analytics begin----
 Strategies are in equilibrium
 NEWGAME:
----Analytics end----

λ: isOptimalSingleDecisionVerbose (pureIdentity 1)
----Analytics begin----
 Strategies are in equilibrium
 NEWGAME:
----Analytics end----

λ: isOptimalSingleDecisionVerbose (pureIdentity 0)
----Analytics begin----
 Strategies are in equilibrium
 NEWGAME:
----Analytics end----
```




### [2022.10.20] First meeting
- Had first discussion with Barnabé
- More precise plan: What do MEV strategies look like in the open games framework, and how do they interact. That is: given an open game description of a contract, how should we think about the strategies of the users and block builders. I could start with a simple toy system and see where that leads us.

**Challenges**
- How to go from smart contract to open game? The *Clockwork Finance* framework seems like a nice approach:
    - Background paper: https://arxiv.org/pdf/2109.04347.pdf
    - Twitter thread: https://twitter.com/kushalbabel/status/1438511507508137987
    - Lecture: https://www.youtube.com/watch?v=n52xBSk2TSs
    - Discussion (from 26:35): https://www.youtube.com/watch?v=W3GOGesPKlw
    - This uses the *K*-framework. 
        - Very long introduction: https://www.youtube.com/watch?v=VlQMi_N42B8
        - very short introduction: https://www.youtube.com/watch?v=eSaIKHQOo4c
- Who are the players in this game? 
    - Users: send transactions that can lead to MEV opportunities
    - Builders: Have the power to extract MEV
    - Contracts: also have 'strategies'--can respond to states and contexts
    - The MEV calculator/searcher? Or should I assume the existence of an MEV oracle?
- What do MEV strategies actually look like in practice? 
- Install Haskell and the Open Game engine



### [2022.10.18] Initial note
This is mostly a placeholder for now. Further development updates will be available here. Initial idea: discuss the usage of the Open Game engine (https://github.com/jules-hedges/open-games-hs) with Barnabe Monnot. A demo is presented from 3:51 on here: https://www.youtube.com/watch?app=desktop&v=v3Fj1GQ0aPI

**Relevant background material**:
- [Bayesian Open Games](https://arxiv.org/abs/1910.03656), 
- [Composing games into complex institutions](https://arxiv.org/pdf/2108.05318.pdf)
- [Compositional Game Theory](https://arxiv.org/abs/1603.04641)
- There seem to be some examples based on staking [here](https://github.com/philipp-zahn/open-games-hs/tree/master/src/Examples/Staking), but I do not really know what they implement. 