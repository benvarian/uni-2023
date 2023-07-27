- starts from a given node and finds all its reachable nodes and the set of relationships that connect the nodes together with the minimum possible weight 
- similar to dijstra's single source shortest path algorithm, but rather than minimisng the total length of a path ending at each relationship, it minimises the length of each relationship individually 
- prims algorith operates as follows 
	- start with a chosen node 
	- the relationship with the smallest weight connected to that node is added to the tree, along with its connected node 
	- repeat this process, always choosing the minimal-weight relationship that joins any node not already in the tree
	- when there are no more nodes, the tree is the mst 

- ![[Screenshot 2023-05-31 at 1.15.31 pm.png]]

- ![[Screenshot 2023-05-31 at 1.15.43 pm.png]]
