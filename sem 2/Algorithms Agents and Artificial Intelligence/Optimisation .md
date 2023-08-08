---
tag: Lecture
---
## Different types of algorithms
- greedy 
	- build solution bit by bit 
	- at each step make optimal choice for next bit
- dynamic 
	- recursive rules for problem, then optimise the algorithm by eliminating repeated work
- approximation 
	- return good solution but not the best one
	- operate very quickly
- gradient based search 
	- take known solutions and try to improve them

optimisation problems 
- trying to find a solution that performs well that meets a certain criteria that is set

greedy algortihms are often fast 

vertext cover is an example of Np-hard problem becuase it is a non-deterministc algorithm

## P vs NP
P
- if there is a deterministic algorithm that solves x and that runs in prolynomial time 
- these are polynomial time problems, often called feasible or tractable 
NP
- if there is a non-deterministic algorithm that solves x and that runs in polynomial time
- often called infeasible or intractable 
- require lucky guesses to work efficiently

## travelling salesman
- another example of a NP problem

## how hard are Np problems 
- there is no known polynomial-time algorithm for x
- the only known algorithms take exponential time 
- if you could solve x in polynomial time, then you could solve them all in polynomial-time

## longest common subsquence 
- given two sequences X and Y, what is their longest common subsequence
- **a subsequence of X is X with zero or more items omitted** 
- so LCS of ABCBDAB and BDCABA are 
	- BCBA, BCAB, BDAB

## recursive relationship


## dynamic programing
- can be applied to 
	- recursive sub-structure 
	- overlapping sub-problems
- basic principle is known as memoisation
	- when we evaluate an application, you remember the result so we dont have to evaluate it again


### populating the table
- ![[Screenshot 2023-07-31 at 3.52.29 pm.png]]
- ![[Screenshot 2023-07-31 at 4.03.31 pm.png]]
- only diagonal cells 
- only take cells that match

## The 0-1 knapsack problem
- set of items X, each with a weight and a value, a given knapsack that can hold weight w, find X' ⊆ X such that 
	- the items in X' fit into K and the total value of the items in X' is maximised

## linear programming
- linear programming problem is characterised by 
	- cost vector 
	- bounds vector
	- an n x m array of constraint coefficients a(ij)
- all linear programming problems can be solved by the simplex algorithm, which has exponential complexity but is genereally feasible in practice


## approximation algorithms 
- that produces solutions to NP-hard problems 
- performance is often described by the ration A(I)/OPT(I)
	- A(I) = value returned by A
	- OPT(I) = the optimum value if known
	- sometimes known bound is substituted for OPT(I)

## greedy approximation for TSP
- nearest neighbour (NN)
	- start at a random chosen city 
	- visit next closest un-visited city 
- NN is O(n^2)