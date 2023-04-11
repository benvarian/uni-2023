## 5.1 network layer design issues 

### 5.1.1 store and forward packet switching 
- ![[Screenshot 2023-04-11 at 3.39.07 pm.png]]
- the equipment is used as follows 
	- a host with a packet to send transmits it to the nearest router, either on its own LAN or over a point-to-point link to the ISP.
	- the packet is stored there until it has fully arrived and the link has finished its processing by verifying the checksum
	- then it is forwaded to the next router along the path until it reaches the destination host, where it is delivered 
	- this is called store-and-forward packet swtiching 

### 5.1.2 services provided to the transport layer 
- services need to be designed with the following goals in mind 
	- the services should be independent of the router technology 
	- the transport layer should be shielded from the number, type and topology of the routers present 
	- the network addresses made available to the transport layer should use a uniform numbering plan, even across LANs and WANs

### 5.1.3 implementation of connectionless service 
- if connectionless service is offered, packets are injected into the network individually and routed independently of each other 
	- the packets are frequently called datagrams and the network is called a datagram network 
- if connection oriented service is used, a path from the source router all the way to the destination router must be established before any data packets can be sent 
	- this connection is called VC (virtual circuit)
- how does a datagram network work?
	- ![[Screenshot 2023-04-11 at 3.56.13 pm.png]]
	- suppose that the process P1 has a long message for P2 on host H2
	- the transport layer code runs on H1, typically within the operating system 
	- it prepends a transport header to the front of the message and hands the result to the network layer
	- **the algorithm that manages the tables and makes the routing decisions is called the routing algorithm.** 

### 5.1.4 implementation of connection oriented service 
- for a connection oriented servcie, we need to have a virutal circuit network 
- the idea behind virtual networks is to avoid having to choose a new route for every packet that gets sent 
- with connection oriented service, each packet carries an identifier telling which virtual circuit it belongs to
- an example of connection oriented network service is MPLS (MultiProtocol label switching). It is used withing isps, with IP packets wrapped in an MLPS header having a 20-bit connectoin identifier or label.

### 5.1.5 comparison of virutal ciruit and datagram networks 
- ![[Screenshot 2023-04-11 at 4.07.04 pm.png]]
- inside the network several trade-offs exist between virutal circuits and datagrams
- one tradeoff is setup time versus adress parsing time 
- using virtual circuits requires a setup phase which takes time and consumes resources 
- however once the price is paid, figuring out what to do with a data packet in a virutal circuit is easy, the router just suses the cirucuit number to index into a table to find out where the packet goes 
- in a datagram network no setup is needed but a more complicated lookup procedure is required to locate the entry for the destination 


## 5.2 routing algorithms in a single network 
- main function of the network layer is routing packets from the source machine to the destination machine
- if the network uses datagrams interally, the routing decisions must be made anew for every arriving packet since they best route may have changed since last time 
- if the network uses virtual circuits internally, routing decisions are made only when a virtual circuit is being set up, so data packets follow the already established route, sometimes called session routing 
- once can think of a router having two processes inside it 
	- one of them handles each packet as it arrives, looking up the outgoing line to use for it in the routing tables, "**forwading**"
	- filling in and updating the routing tables 
		- certain properties are desirable in a routing algoritm 
			- corrrectness
			- simplicity 
			- robustness 
				- the algorithm needs to be able to cope with changes in the topology and traffic without requiring all jobs in all hosts to be aborted 
			- stability 
				- a stale algorithm reaches equilibrium and stays there 
			- fairness 
			- efficiency 
- rotuing algoritms can be grouped into 2 types 
	- non-adaptive 
		- dont base their routing decisions on any measurements or estimates  of the current topology and traffic 
		- instead the choice of route is computed in advance 
		- sometimes called static routing 
			- doenst respond to failures
			- best use when the route is obvious 
	- adaptive 
		- change their routing decisions to reflect changes in the topology

### 5.2.1 the optimality principle 
- if router j is on the optimal path from router I to router K, then the optimal path from J to K also falls along the same route 
- to see this, call the part of the route from I to Jr1 and the rest of the toure r2.
- if a route better than r2 existed from J to K, it could be concatendated with r1 to improve the route from I to K, contradicting our statement that r1r2 is omtimal 
- as a direct consequence of the optimality principle, we can see that the set of optimal routes from all sources to a given destination form a tree rooted at the destination
- such a tree is called a sink tree
- ![[Screenshot 2023-04-11 at 4.52.53 pm.png]]

### 5.2.2 shortest path algorithm 
- the concept of the shortest path algorithm, the paths ABC and ABE are equally as long 
- ![[Screenshot 2023-04-11 at 4.54.36 pm.png]]
- other things can be added like delay of each transmission and so on 
- with this type of graph labeling the shortest path is the fastest path rather than the path with the fewest edges or kilometers 

### 5.2.3 flooding 
- each router must make decisions based on local knowledge, not the complete picture of the network 
- flooding, in which every imcoming packet is sent out on every outgoing line except the one it arrived on 
- creates vast amount of duplicate packets 
- have routers keeps track of which packets have been flooded, to avoid sending them out a second time, have each router put a sequence number in each packet it receives from its hosts 
- each router then needs a list per source router telling which sequence numbers originating at that source have already been seen, if any incoming packet is on the list, it is not flooded 
- important uses 
	- ensures that a packet is delivered to every node in hte network, may be wasteful if there is a single destination that needs the packet 
	- tremendously robust 
		- even if a large number of routers are blown, flooding will find a path if one exists 
		- used as a metric against which other routing algorithms can be compared 
- **always chooses the shortest path because it chooses every possible path in parallel**


### 5.2.4 distance vector routing 
- operates by having each router maintain a table giving the best known distance to each destination and which link to use to get there
- these tables are updated by exchanging information with the neighbours 
- eventually each router will knwon the best link to reach each destination 
- count to infinity problem 
	- the settling of routes to best paths acorss the network is called convergence 
	- DVR has a serious problem 
		- it reacts rapidly to good news but slowly to bad news 
	- no router ever has a vlue more than one higher than the minimum of all its neighbours 
	- gradually all the routers work their way up to infinity, but the number of exchanges required depends on the numerical value used for infinity
	- for this reason set infinity to the longest path value + 1

### 5.2.5 link state routing 
- IS-IS and OSPF are used widely in the internet today 
- the idea 
	1. discover its neighbours and learn their network addresses 
	2. set the distance or cost metric to each of its neighbors 
	3. building link state packets
		- hardest part is when to rebuild the packet
			- options are events like a neighbour disconnecting or something going down
	4.  send this packet to and receive packets from all other routers 
	5. compute the shortest path to every other router 


### 5.2.6 hierarchial routing within a network 
- the routers are divided into regions or areas 
	- each router knows all the details about how to route packets to destinations wihtin its own region but knows nothing about the internal structure of other regions 

### 5.2.7 broadcast routing 
- sending a packet to all destinations simultaneously is called broadcasting 
- for the source to simply send a distinct packet to each destination
- an improvement on above is multidestination routing, each packet contains either a list of destinations or a bit map indicating the desired destinations 
	- when a packet arrvies at a router, the router checks all the destinations to determine the set of output lines that will be needed 
	- the router generates a new copy of the packet for each output line to be used and includes in each packet only those destinations that are to use the line 
	- the destination set is partitioned among the output lines 

### 5.2.8 multicast routing 
- requires some way to create and destroy group and to identify which routers are members of a group
- multicast routing schemes build on the broadcast routing schemes, sending packets along spanning trees to deliver the packets to the members of the group while making efficient use of bandwith 
- the best spanning tree to use depends on whether the group is dense, or sparese 

### 5.2.9 anycast routing 
- a pacekt is delivered to the nearest member of a group
- why would we want this 
	- sometimes nodes provide a service, such as time of day or content distribution for which it is getting the right information that matters, not the node that is contacted as any node will do

## 5.3 traffic management 
- congestion collapse 
	- performane plummets as the offered load increases beyond the capacity 
	- with to much load the amount of well sent packets decreases 
- difference between congestion control, traffic managment and flow control
	- traffic 
		- make sure the network is able to carry the offered traffic
		- can be performed by devices within the network or by the senders of traffic 
	- congestion 
		- controls all behaviour of all the hosts and routers 
	- flow 
		- the traffic between a particular sender and a particular receiver 
		- makiing sure that the sender is not transmitting data faster than the receiver can process it 

### 5.3.2 approaches to traffic managment 
- links and routers that are regulararly utilised are upgraded at the earliest opportunity, this is called provisioning and happens on a time scale of months, driven by long-term traffic trends 
- traffic aware routing 
	- regulating the average rate and burstiness of a flow of data that enters the network
- sometimes the only way to beat back congestion is though decreasing the load. an can be done by not allowing new connections if they would casue the network to become congested. this is called admission control 
- the network can requests sources to slow down the sending rates, or it can simply slow down the traffic itself, which is refered to as throttling
- load shedding 
	- when a router becomes so overflowen with packets it simply throws them away 
	- this is a last resort 
- token buckets vs leaky buckets 
	- ![[Screenshot 2023-04-11 at 9.05.14 pm.png]]
	- leaky bucket means that when a packet is sent to a host there has to be room to accomodate for it otherwise itll get thrown out 
	- token bucket means that a ceratain amount of tokens cant accumulate in the bucket, which means its different as with leaky bucket if it gets to full it can simply discard packets but this option cant 

- random early detection 
	- routers maintain a running average of their queue lengths 
	- when the avg length on some links exceed a threshold, the link is said to be congested and a small fraction of the packets are dropped at random 

- choke packets 
	- the router selects a congested packet and sends a choke packet back to the source host, giving its destination found in the packet 
	- the original packet should be tagges so that it wont send any more packets 

- explicit congestion notification 
	- instead of genreating more packets to warn of congestion a router can tag any packet it forwards to a singal that its experiencing congestion
	- when the network delivers the packet, the destination can note that tehre is congestion and inform the sender when it sends a reply packet 

## 5.4 quality of service and application QOE

### 5.4.1 application Qos Requirements 
- a stream of packets is referred to as a flow 
- the needs for each flow can be characterised by four primary parameters 
	- bandwitdth 
	- delay 
		- nothing is really that sensitve to delays but it would be good to not have long amounts of delays for some things 
	- jitter 
		- the variation in the delay or packet arrival times 
	- loss 
- example of an ATM 
	- they support 
		- constant bit rate 
		- real-time variable bit rate 
		- non-real-time variale bit rate 
		- available bit rate 

### 5.4.2 overprovisioning 
- an easy solution to provide good quality of service is to build a network with enough capacity for whatever fraffic will be thrown at it 