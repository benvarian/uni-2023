## generalised search algorithm 
- idea
	- we are in a state
	- the state will usually offer several possible actions 
	- choose once action to explore first 
	- keep the state and the use the other actions to explore later, in case the first doesnt deliver 
- the action that gets selected is determined by a search strategy 
- ![[Screenshot 2023-09-12 at 11.32.46 am.png]]


## comparing search strategies 
- completeness 
	- is the strategy guaranteed to find a solution?
- optimality 
	- is the strategy guaranteed to find the optimal solution 
- time complexity 
	- how long does the strategy take to find a solution 
- space complexity 
	- how much memory is needed to conduct the search 
- often expressed as 
	- b = maximum branching factor of the tree
	- m = maximum depth of the search tree
	- d = depth of the least-cost solution

## uninformed search strategies 
- breadth first search 
	- starts at tree root and explores all nodes at the present depth prior to moving onto the nodes at the next depth level 
	- uses a queue = FIFO
- uniform cost search (cheapest first search)
	- minimal total cost from starting to end node basically
	- directional 
	- holds a list called visited to track with nodes have been visited
		- cant go back to the original node as its already been visited
	- if the node gets visited by an alternative route, its a dead end 
- depth first search 
	- uses stack = LIFO
	- may loop back to a node that you have already visited, need to implement a checker so it doesn't loop back basically 
	- doesn't care about the cost 
	- may tend to be a longer path as its not optimal in cost and not optimal in number in actions 
	- saves on space in memory
- depth limited search 
	- its different from the usual depth first search as it poses a boundary or limit on the depth that can be searched
	- stops the infinite iterations basically
- iterative deepening depth first search 
	- same as depth but slowly increases the limit to assure of a found goal
- bi-directional search 
	- generally you'll have point 0 branching out 2 points, and from those 2 points 2 trees will spawn out 
	- two iterations of breadth first search occur at the same time, start one at start vertex and one at the end vertex 
	- used to find the shortest distance between a fixed start vertex and end vertex 