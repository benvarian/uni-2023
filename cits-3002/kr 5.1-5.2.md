
## 5.2 routing algorithms
- centralised routing algorithm
	- computes the least cost path between a source and destination using complete, global knowledge about the netowkr
	- the algoritm has complete information about connectivity and link costs 
	- algorithms with global state information are often referred to as link-state (LS) algorithms, since the algorithm must be aware of the cost of each link in the network 
- decentralised routing algorithms 
	- carried out in a iterative, distributed manner by the routers 
	- each node begins with only the knowledge of the costs of its own directly attached links 
	- then through an iterative process of calculation and exchange of information with its neighboring nodes, a node gradually calculated the least cost path to a destination or set of destinations 
- static routing algorithms 
	- change very slowly over time, often as a result of human intervention
- dynamic routing algorithm 
	- change the routing paths as the network traffic loads or topology change 
	- can run either perioidcally or in direct response to topology link cost changes 
	- more susceptible to problems such as routing loops and route oscillation 
- load-sensitive algorithm 
	- link costs vary dynamically to reflect the current level of congestion in an underlying link 
	- if a high cost is associated with a link that is currently congested, a routing algorithm will tend to choose routes around such a congested link 

### 5.2.1 the link state routing algorithm 
- the network topology and all link costs are known
- in practice this is accomplished by having each node broadcast link-state packets to all other nodes in the network, with each link state packet containing the identities and costs of its attatched links 
- uses things like Dijkstras algorithm and uses the property of that after the kth iteration of the algorithm, the least-cost paths are known to k destination nodes 


### 5.2.2 the distance vector routing algorithm 
- is iterative, asynchronous and distributed 
- it is distributed in that each of the  nodes receives some information from one or more of its directly attached neighbours, performs a calculation and then distributes the results of its calculation back to its neighbours 
- it is iterative in that it continues until no more information is exchanged between neighbours 
- is asynchronous in that it doesnt require all of the nodes to operate in lockstep of each other 

#### a comparison of LS and DV routing algorithms 
- in the Dv algorithm
	- each node talks to only its directly connected neighbour
	- but provides its neighbour with least-cost estimates from itself to all the nodes that it knows about in the network
- the LS algorithm
	- requires global information
	- when implemented into each router, each node would need to communicate with all other nodes, but it tells them only the costs of its directly connected links 
- message complexity (N = nodes, E = set of edges)
	- LS requires each node to know the cost of each link in the network, it requires O(N E) messages to be sent, whenver a link cost changes, the new link cost must be sent to all nodes. 
	- DV requires message exchanges between directly connected neighbours at each iteration, when link cost changes the DV will propagate the results of the changed link cost only if the new link cost results in a changed least-cost path for one of the nodes attached to that link
- speed of convergence 
	- LS is an O(N^2) algorithm requiring O(N E) messages
	- DV can converge slowly and can have routing loops while the algorithm is converging, suffers from the count to infinity problem
- robustness 
	- LS, a router could broadcast an incorrect cost for one of its attached links, a node could also corrupt or drop any packets it received as part of an LS broadcast, LS node only computing its own forwading tables while other nodes are performing similar calculations for themselves, this means route calculations are somewhat separated under LS, providing a degree of robustness 
	- DV, a node can advertise a incorrect least-cost paths to any or all destinations. at each iteration a nodes calculation in DV is passed on to its neighbor and then indirectly to its neighbours neighbour on the next iteration. in this sense an incorrect node calculation can be diffused through the entire network under DV