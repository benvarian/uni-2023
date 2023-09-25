---
tag: Lecture
---
## uninformed search
- select nodes for expansion on the basis of distance/cost from the start date
- only information contained in graph 
- no indication of distance to go

## informed search
- selects nodes for expansion on the basis of some estimate of distance to the goal state
- requires additional information:
	- heuristic rules 
	- evaluation function

## greedy search
- selects the unvisited node with the smallest estimate 
- "one that appears closest to the goal"
- eval function is the estimate of the cost of getting from n to the goal 
- complete: not always 
- optimal: returns first goal found, "not always the best goal"
- time O($B^M$)
- space: $O(B^M)$ 

## a* search
- greedy minimises estimate path-cost to goal
- uniform cost search minimises path-cost from the start
- can we get the best of both worlds?
	- yes 
		- use estimate of total path cost as our heuristic 
- $f(n) = g(n) + h(n)$
	- g(n) = actual cost from start to n
	- h(n) = estimated cost from n to goal
	- f(n) = estimated total cost from start to goal via n
- reduces search space 
	- a* > dijkstras 
	- as dij doesn't know which is the best way straight away
- is complete and optimal under two conditions 
	- heuristic must be admissible 
	- cost along a given path must be monotonic 
- heuristic (h) is admissible iff $h(n) ≤ h^* (n)$ 
	- $h^*$ is the actual path cost from n to the goal 
- heuristic is monotonic iff $h(n) ≤ c(n,a,n') + h(n')$ 
	- n' is a successor to n by action a 
	- the triangle inequality
	- n to the goal  "directly" should be no more than n to the goal via any successor n'

## a* example of how it works
- ![[Screenshot 2023-09-12 at 11.03.18 am.png]]
	- G = top left 
	- H = top right 
	- F = middle
- position a, has values that determine how close it is to the destination, choses the box with the lowest F cost, iterates over until it gets to the end 
- when theres F costs with equal values, you pick the lowest H cost

### a* view operationally 
- complete 
- optimal
- time O(x)
- space O(x)

## assessing heuristics 
- two possible heuristics are 
	- $h_1(n)$ = number of misplaced titles 
	- $h_2(n)$ = total amount of manhattan distance of all tiles 

## heuristic quality 
- quality of heuristic can be expressed as its effective branching factor 
- assume a* visits N nodes, and finds solution at depth d
- the effective branching factor b* is the branching factor of "perfect tree" with these measurements 
- b* tends to be fairly constant over problem instances 

## heuristic dominance 
- say that $h_2$ dominates iff they are both admissable, and $h_2(n) ≥ h_1(n)$
- if $h_2$ dominates $h_1$, then A* with $h_2$ will usually visit fewer nodes than A* with $h_1$
- ![[Screenshot 2023-08-21 at 3.56.29 pm.png]]
- normally favour a dominant heuristic

## deriving heuristics 
- given a problem p, a relaxed version of p' of p is derived by reducing restrictions on operators 
	- then the cost of an exact solution to p' is often a good heuristic to use for p


## memory bounded a*
- solved space problem for uniformed strats by iterative deepening 
- can do same here 
	- IDA* uses the same idea as ID
	- but instead of imposning a depth cut off, it imposes an f-cost cut off
- IDA* performs depth limit serach on all nodes n, such that f(n) ≤ k.
	- if fails 
	- increases k and tries again

### simplified memory bounded A*
- SMA* expands the most promising node until memory is full
	- then drops a node in order to generate more nodes and continue the search
- expands the most promising node until memory is full
	- then it must drop a node in order to generate more nodes and continue the search
- SMA* drops the least promising node in order to make space 
- when a node x is dropped, the f-cost of x is backed up in x's parent node 

## sma* performane
- complete 
	- if a linear path to depth d can be stored
- optimal
	- with memory available 
- time 
	- O(x), x = number of nodes with f(n) ≤ $f^*$ 
- still robust search process for many problems 