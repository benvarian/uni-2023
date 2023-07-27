
- calculates the shortest path between a pair of nodes 
- operates as follows 
	- finds the lowest-weight relationship from the start node to directly connected nodes 
	- moves to the closest node, keeping track of the weights 
	- performs the same calculation, but now as a cumulative total from the start node 
	- repeats, choosing the lowest weighted cumulative path in each iteration 

![[Screenshot 2023-05-31 at 12.56.18 pm.png]]

![[Screenshot 2023-05-31 at 12.56.42 pm.png]]

- running it in neo4j 
	- ![[Screenshot 2023-05-31 at 12.56.58 pm.png]]