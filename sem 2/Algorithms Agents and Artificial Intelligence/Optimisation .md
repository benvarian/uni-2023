---
tag: Lecture
---
## Different types of algorithms
- greedy 
	- build solution bit by bit 
	- at each step make optimal choice for next bit
	- **follows the problem solving heuristic of making the locally optimal choice at each stage**
		- **in many problems, a greedy algorithm doesn't produce an optimal solution, but can yield locally optimal solutions that approximate a globally optimal solution in a reasonable amount of time**
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

vertex cover is an example of Np-hard problem becuase it is a non-deterministc algorithm

## problem with greedy algorithms 
- the locally optimal choice reduces our options for later choices 

## P vs NP
P
**- if there is a deterministic algorithm that solves x and that runs in prolynomial time** 
- these are polynomial time problems, often called feasible or tractable 
NP
**- if there is a non-deterministic algorithm that solves x and that runs in polynomial time**
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
	- when we evaluate an application, you remember the result so we don't have to evaluate it again
- maintain a table of applications that have been evaluated
	- for each new application, we check to see if we have done it previously 
		- if we have, look up result 
		- if we haven't, do the evaluation and store the result 


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
- eg: an approximation algorithm for travelling salesman would return some circular tour, hopefully a good tour, but not necessarily the best tour 
- performance is often described by the ration A(I)/OPT(I)
	- A(I) = value returned by A
	- OPT(I) = the optimum value if known
	- sometimes known bound is substituted for OPT(I)

## greedy approximation for TSP
- one simple algorithm is nearest neighbour (NN)
	- start at a random chosen city 
	- visit next closest un-visited city 
- NN is O(n^2)

## TSP theorems  (traveling salesman problem)
- theorem 
	- for any constant $k > 1$ there are instances of the TSP such that NN(I) ≥ k OPT(I)
- suppose A is a polynomial time approximation algorithm for the TSP such that A(I) ≤ OPT(I) for some constant k and for all instances I
	- then there exists a polynomial time algorithm to solve the TSP

## minimum spanning trees for TSP 
- the algorithm is guaranteed to find a TSP tour for I that is at most twice the optimal length 
	- find a minimum spanning tree for I
	- do a depth first search on the tree
	- visit the vertices in order of discovery time 

## insertion algorithms for the TSP 
- maintain a cycle through a subset of vertices, and insert new vertices into this cycle 
- at each stage we apply an insertion method, M, that inserts on vertex into a closed tour C
	- M selects an unused vertex x, then it inserts x into C at its best position 
- three common insertion methods 
	- Nearest insertion: choose the x closest to C
	- Farthest insertion: choose the furthest from C
	- Random insertion: choose x randomly 

### Cheapest insertion 
- with this method, you search through all edges and all vertices ato find the pair that minimises 
	- ![[Screenshot 2023-09-14 at 1.58.56 pm.png]]
- the previous three methods work in $O(n^2)$ time 
	- separates choosing a vertex from choosing an insertion point
	- cheapest insertion seems to require at least an additional factor of (logn)

### Iterative improvement 
- changing a few edges here and there using a greedy approach
- leads to the idea of iterative improvement 
	- create a feasible solution 
	- modify it slightly to improve it 
- requires 
	- a rule for changing one feasible solution to another 
	- schedule for deciding which changes to make 

### improving tsp tours 
- basic move, is deleting two edges and replacing them with two non-edges 
- ![[Screenshot 2023-09-14 at 2.02.51 pm.png]]

### 2-opt
- in every iteration, examines every pair of edges in a tour, and performs an exchange if it would improve the tour 
- after the procedure terminates, the resulting tour is called 2-optimal 

### k-optimal 
- a tour that cannot be improved by a k-edge exchange 
- its unusual to go beyond 3-optimal because of the expense and because of diminishing returns 

## state space graph 
- of an instance I of the TSP is denoted by S(I)
	- the vertices of S(I) comprise of all feasible tours for I
	- two vertices in S(I) are connected iff they can be obtained from each other by the edge exchange procedure described previously 
- each vertex of S(I) has an associated cost which is the length of the tour T
- to completely solve the instance I, it requires finding which of the (n-1)! vertices of S(I) has the lowest cost 

## gradient based search 
- we have a current tour T, and in each iteration 
	- we generate a neighbour T' of T, and 
	- we decide whether or not to "move" to T'
- known as hill-climbing 
	- generate neighbours T' of T and move the first one with lower cost than T
- process then terminates when it is at a T that has no neighbours of lower cost 
	- T is then called 2-opt 
- obvious variant is to always choose the best move at each step 

## local optima 
- a hill-climb will always finish at a vertex that has a lower cost than its neighbours 
- the state-space graph has an enormous number of local optima, only one of which is the global optimum that we would like to reach 

### Simulated annealing 
- tries to avoid local optima by allowing the search process to take backward moves 
- each iteration goes like 
	- random gen neighbour T' of T
	- if cost(T') ≤ cost(T), accept T'
	- if cost(T') > cost(T), accept T' with probability p
- **intended to move us to a new part of the space so we can search there**
- use a temperature variable t which goes down as time advances, and we relate p to t


### Tabu search 
- tries to avoid two weaknesses 
	- inability of hill-climbing to escape local optima 
	- early randomness of simulated annealing 
- aim is to spend most of the time exploring local optima, whilst retaining the ability to escape them
- keep a 'tabu list' that details the last h vertices that have been visited, and at each iteration 
	- select the best neighbour T' of T
	- if T' is not on the tabu list, move to T' and update the list 
- **prevents the search form spending too much time at one local node optimum, forcing it to visit other parts of the search space**

### genetic algorithms 
- try to avoid getting stuck in local optima by maintaining a population of solutions 
- at each iteration, the population size n is used to create n new solutions, and the best n of these "survives" into the next generation 
