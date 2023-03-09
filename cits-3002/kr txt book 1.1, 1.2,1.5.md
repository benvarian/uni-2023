# 1.1
## what is the internet 
- the basic hardware and software components that make up the internet
- provides services to distributed applications

### 1.1.1 a nuts and bolts description 
- all devices are either host or end systems 
- ![[Screenshot 2023-03-08 at 1.11.26 pm.png]]
- end systems are connected togehter by a network of communication links and packet switches 
- transmission rate of a link measured in bits/second
- when one end system has data to send to another end system, the sending end system segments the data and adds header bytes to each segment, the resulting packages of information are knows as **packets**, are then sent trough the network to the destination end system, where they are they reassembled into the original data form. 
- two most prominant types of packet swtiches in todays internet are routers and link-layer swtiches 
	- both forward packets toward their ultimate destinations.
	- link-layer are typically used in access networks
	- routers used in the network core 
- the sequence of comm links and packet switches traversed by a packet from the sending end system to the receiving end system is known as the **path** or route **through** the network 
- example
	- Packet-switched networks (which transport packets) are in many ways similar to transportation networks of highways, roads, and intersections (which transport vehicles). 
	- Consider, for example, a factory that needs to move a large amount of cargo to some destination warehouse located thousands of kilometers away. At the factory, the cargo is segmented and loaded into a fleet of trucks. 
	- Each of the trucks then independently travels through the network of highways, roads, and intersections to the destination warehouse. 
	- At the destination warehouse, the cargo is unloaded and grouped with the rest of the cargo arriving from the same shipment. 
	- Thus, in many ways, packets are analogous to trucks, communication links are analogous to highways and roads, packet switches are analogous to intersections, and end systems are analogous to buildings. 
	- Just as a truck takes a path through the transportation network, a packet takes a path through a computer network.
- end systems run protocols that control the sending and receiving of information within the internet. The **Transmission Control Protocol (TCP)** and the **Internet Protocol** are 2 of the most important in the internet. 
- the ip protocol specifies the format of the packets that are sent and received amount routers and end systems 

- network protocols
	- 
