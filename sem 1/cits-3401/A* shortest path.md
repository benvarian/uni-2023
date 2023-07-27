
- improves on dijkstra's by finding shortest paths between two nodes more quickly 
- allows the inclusion of extra information that the algorithm can use as part of a heuristic function to determine which nodes to explore next 
- selects the path that minimises the following function 
	- f(n) = g(n) + h(n)
	- g is the cost of the path from the source to node n
	- h is the estimated cost of the path from node n to the destination node, as computed by a heuristic 

- use teh geospatial distinace as the heuristict, using the haversine formula 
- must ensure the lat and long properties are included in our projection 
-  ![[Screenshot 2023-05-31 at 1.00.56 pm.png]]

- ![[Screenshot 2023-05-31 at 1.01.10 pm.png]]