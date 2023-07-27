
- non adaptive algorithms 
	- the choices of routes between each two hosts are computed in advance and loaded into each host in the whole network before the network is "brought-up"
	- non adaptive choices are often termed static routing 
- adaptive algorithms 
	- are characterised by their attempts to adjust their route choices based on their current knowledge of the network topology
	- there are 3 type of adaptive algorithms 
		- global algorithms use information periodically collected from the whole network 
		- local algorithms use only the information that each router knowns about itself, such as queue lengths and waiting times, and 
		- combined algorithms use some of both global and local information 
	- adaptive choices are often termed dynamic routing 


![[a naive non-adaptive routing algorithm - flooding]]

![[improved flooding algorithms]]