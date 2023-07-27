
- cypher allows us to specify a variable path length 
	- (node)-[*5]->(node) - path of length 5
	- (node)-[*..5]->(node) - paths of length less than 5 
	- (node)-[*5..]->(node) - paths of length 5 or more 
	- (node)-[*3..5]->(b) - paths from length 3 to 5

- the most simple function with is apoc.path.expand, which allows us to traverse paths based on relationship filters or node filters 
- specify the start node, relationship filter, label filter, and path length 
	- ![[Screenshot 2023-05-31 at 12.30.58 pm.png]]
	- ![[Screenshot 2023-05-31 at 12.36.01 pm.png]]