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
	- all activity that is exchanged in the internet that involved 2 or more communicating remote entitie is goverend by a protocol 
	- definition
		- defines the format and the order of messages exchanged between two or more communicating entities, as well as the actions taken on the transmission and/or receipt of a message or other event 


# 1.2 the network edge
- end systems are referred to as hosts becuase they host application programs such as a web browser program 

## 1.2.1 access networks 

## 1.5 protocol layers and their service models 

### protocol layer
- each protocol belongs to one of the layers 
- each layer provides its service by 
	- performing certain actions within that layer and by 
	- using the services of the layer directly below it 
- both physical and data link layers are responsible for handling communciation over a specific link, typically implemented in a NIC associated with a given link 
- ![[Screenshot 2023-03-14 at 1.15.20 pm.png]]
- five layer internet protocol stack 
	- application layer
		- where network applications and their application layer protocols reside 
		- includes HTTP, SMTP, FPT protocols 
	- transport layer 
		- in the internet there are two transport protocols, TCP and UDP 
		- TCP provides a connection-oriented service to its application 
		- this service includes guaranteed delivery of application layer messages to the destination and flow control 
		- TCP also breaks long messages into shorter segments and provides a congestion control mechanism, so that a source throttles its transmission rate when the network is congested 
		- the UDP protocol provides a connectionless servcie to its applications 
		- no-frills service that provides no reliability, no flow control and no congestion control. 
		- refer to the transport layer as a segment 
	- network layer 
		- responsible for mvoing network-layer packets known as datagrams from one host to another 
		- the internet transport layer protocol in a source host passes a transport layer segment and a destination address to the network layer
		- the network layer then provides the service of delivering the segment to the transport layer in the destination host 
		- includes the ip protocol
		- also contains routing protocols that determine the routes that diagrams take between soruces and destinations.
	- link layer 
		- to move a packet from one node to the next node in the route, the network layer relies on the services of the link layer 
		- at each node, the network layer passes the diagram down to the link layer, which delivers the datagram to the next node along the route. at this next node, the link layer passes the datagram up to the network layer
		- examples of link layer include 
			- ethernet
			- wifi 
			- the cable access network's DOCSIS protocol 
		- refer to link layer packets as frames
	- physical layer 
		- the responsibility is to move the individual bits within the frame from one node to the next 
- the osi model 
	- application layer
		- where network applications and their application layer protocols reside 
		- HTTP
		- SMTP 
		- FTP
	- presentation layer 
		- provide services that allow communcating applications to interpret the meaining of data exchanged 
		- these services inlcude data compression and data encryption as well as data description 
	- session layer
		- provides for delimiting and synchronisation of data exchange, including means the measnt to build a checkpointing and recovery scheme 
	- transport layer 
		- transports application layer messages between application endpoints 
		- in the internet there are two transport protocols TCP & UDP. 
		- TPC provides a connection oriented service to its applications, includes guaranteed delivery of aplication layer messages, also breaks longer messages into shorted segmeents 
	- network layer 
		- responsible for moving network layer packets known as datagrams from one host to another 
		- include the IP protocol 
	- data link layer 
		- routes a datagram through a series of routers between the soruce and destination 
	- physical layer 
		- move individual bits within the frame from one node to the next 
