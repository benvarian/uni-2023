---
tag: Lecture
---
## approaches to uncertainty
- Contingency planning 
	- build all possibilities into plan
	- often makes a very large tree 
	- can only guarantee a solution if the number of contingencies is tractable 
- interleaving, or adaptive planning 
	- alternate between planning, acting, and sensing 
	- requires extra work during execution
	- unsuitable for offline planning 
- strategy learning 
	- learn, from examples, strategies that can be applied in any situation 
	- must decide on parameterisation, state-evaluation

## why study games?
- games provide 
	- abstraction of the real world 
	- a way of making incremental, controllable changes 
	- a way of including hostile agents 
- the initial state and the set of actions define a game tree 

## min-max algorithm 
- consider a two-player game between max and min
	- moves alternate between the players 
	- assume it is a zero-sum game 
		- what is good for one player is bad for the other 
	- assume we have a utility function that we can apply to any game position 
		- utility(s) returns $r \in R$ 
		- $\infty$ if s is a win for MAX
		- positive result if s is good for MAX
		- no result = 0, if s is even for both players 
		- negative result if s is good for MIN
		- $-\infty$ if s is a win for MIN

### min-max operation
- imagine the game tree is expanded to some definition of terminals 
- tree is generated top down, starting from current position 
	- then the min-max is applied from the bottom-up
	- from the leaves branching out back to the current position
- **calculating the max value of a player is done in a worst-case approach, for each possible action of the player, we check all possible actions of the other players and determine the worst possible combination of actions** 
	- the move that gives player i the smallest value
	- then we can determine which action player i can take in order to make sure that this smallest value is the highest possible 
- ![[Screenshot 2023-09-12 at 10.20.33 am.png]]
- white picks the value that is greatest, making an advantage for itself 
- black picks the smallest value, as this dis-advantages white more 


### min-max performance 
- complete: yes 
- optimal: yes
- time: $O(b^m)$
- space: $O(bm)$, depth-first search 


## evaluation functions 
- if we cannot expand the tree to terminal nodes, we expand as far as we can and apply some judgement to decide which positions are best 
- **is a function that is used by game-playing programs to estimate the value or goodness of a position in a game tree**

### properties of good evaluation functions 
- usually the quality of the player depends critically on the quality of the evaluation function
- evaluation function should 
	- agree with the utility function on terminal states
	- reflect the probability of winning 
	- be time efficient, to allow maximum search depth


## cutting off search 
- can cut-off search at a fixed depth 
	- works well for simple games 
	- depth-limited search
- required to manage the time taken per move 
- sometimes we are required to manage the time taken for a series of moves 
	- more complicated again

## quiescence 
- a situation where values from the evaluation function are **unlikely** to change much in the near future 
- attempts to emulate the human effect of knowing that a move is bad and abandoning it
	- instructs the agent to search the volatile positions to a greater depth than quiet ones to make sure that there are no hidden traps 
## horizon effect
- because the tree is generally so big in size that a agent has to analyse, the computer is only able to select a small portion of them 
- thus for a computer that is searching through like 5 plies, there is a possibility that it will make a detrimental move, but the effect is not visible because the computer does not search to the depth of the error ("beyond the horizon")

## alpha-beta pruning 
- seeks to decrease the number of nodes that are evaluated by the algorithm 
- it forces a algorithm to stop running when a move has at least one possibility that proves the move to be worse than a previously examined move 
- generally relies on analysing half of branch and making conclusions as to the best option, without actually analysing the rest
	- ![[Screenshot 2023-09-12 at 10.53.26 am.png]]
