
- standard operations to answer queries 
	- measurements 
		- which facts should be reported 
	- filters 
		- what slice of the cube should be used 
	- grouping attributes 
		- how finely should the cube be dices 
		- each dimensions is either 
			- grouping/categorical/discrete attribute 
			- aggregated over 

- efficient processing of OLAP queries 
	- ![[Screenshot 2023-03-27 at 3.20.55 pm.png]]

- using cubes in queries 
	- queries with data cube in SQL server 
	- SELECT ... FROM SALES CUBE BY ....
- creating cross tab with SQL 
	- ![[Screenshot 2023-03-27 at 3.24.24 pm.png]]
	- what about the totals 
		- ![[Screenshot 2023-03-27 at 3.24.49 pm.png]]
	- one solution
		- a big union all 
		- ![[Screenshot 2023-03-27 at 3.25.14 pm.png]]

- rollup vs cube 
	- cube computes enitre lattice 
	- rollup computes one path through lattice 
		- order of group by list matters 
		- groups by all prefixes of the group by list 
	- ![[Screenshot 2023-03-27 at 3.26.27 pm.png]]

- data cube lattice 
	- ![[Screenshot 2023-03-27 at 3.26.39 pm.png]]