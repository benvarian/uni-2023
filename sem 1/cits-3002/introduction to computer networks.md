## textbook readings 
![[kr txt book 1.1, 1.2,1.5]]

![[tan 1.1 -> 1.4]]
## basic networking definitions 
- a computer network is a interconnected collection of autonomous computers 
- computers are considered interconnected if they are capable of exchanging microwaves 
- physically a network is the computers and physial media connecting them
- Logically, a network is the software which connects and secures the computers, their data and services 

## why do users value computer networks
- users can access and create shared, distributed and replicated data from a variety of locations, including mobile and wireless services 
- Streaming services
- users can have their own computer and access shared and possibly distant physical resources 
- networks can provide fault tolerance and load balancing 
	- if some form of hardware fails then logically shadowing and delay-tolerant networking enables data recovery and continuted performance 
- permit centralised facilities
- permit remote collaboration
	- instant messaging, zoom calls 

## research inresets and networking 
- unreliable communication 
	- messages sent over physical media are often lost, so how do we cater for that 
- the supports and study of temporal and spatial decoupling of work patterns and communities 
- privacy and security
	- indsutrys desire to get more data from each person to drive algorithms for figuring out profits 
- parallel programming 
	- writing modelling and imagining the execution of parallel programming is very difficult

## the need for network protocols 
- def: a computer protocol consists of an agreed format for messages, expressed by a packet header, an optional message component, and a set of rules for the exchange of messages between computers 
- we use protocols in almost every activity 
	- web servers 
	- electronic mail and news articles are shared using smpt (simple mail transfer protocol) servers and the NNTP (network news transfer protocol).
- most importantly the protocol messages must 
	- happen in an agreed order 
	- travel from the sender to the correct receivers 
	- contain the correct unambiguous data 
- equally important 
	- time plays a critical role 
	- information will be lost and corrupted and protocols must account for this

## the ISO/OSI reference model 
- with computer networks we required protocols to meet new computers, ask for information, agree to share data etc
- the complexity of protocols can be simplieifed by seperating some of the functions required into different protocls, and isolating "layers of responsbility" into different protocol modules
- a solution to such seperation of responsibilites is provided by the open systems interconnection / international standards organisation 
- standardised in 1983
- today the transmission control protocol/internet protocol (TCP/IP) suite meets nearly all of our networking needs 

### why a layered model? why 7 layers 
- ![[Screenshot 2023-03-04 at 1.12.42 pm.png]]
- the following principles were followed 
	- a layer corresponds to a different level of abstraction
	- each layer provides a well defined, independent function
	- within each layer unique protocol standards should be enforceable 
	- there should be a minimum of traffic between layers/across interfaces 
	- the number of layers should be sufficiently large that distinct functions are in different layers and that there are not too many layers for the whole model to become unmanageable 

### the ISO/OSI reference model - layer upon layer
- ![[Screenshot 2023-03-04 at 1.15.06 pm.png]]
- The Physical Layer
	- responsible for transmitting a raw bit stream over the physical communication medium 
	- as such it is concerened with the electrical and mechanical interface between the data and the physical medium 
	- presents a bit stream to the layer above 
- The data link layer 
	- ![[Screenshot 2023-03-04 at 1.16.15 pm.png]]
	- takes teh bit stream from the physical layer and constructs logical chunks of data termed frames 
	- the purpose of framing is to ensure the reliable transmission of information by performing limited error detection and recovery 
- The network layer 
	- is responsible for providing the connection between "end systems" across a network 
	- these connections might include multiple, intermediate links and are intended to be independent of the networks used to transmit the data 
	- functions include 
		- routing
			- deciding how to transmit frames between soruce and destination using addresses 
		- relaying
			- enables data transfer across intermediate networks 
		- flow control
			- matches traffic flow with the physical capacity of a transmission path
		- sequencing 
			- control ordering of frames across a network 
- the transport layer 
	- provides a reliable end-to-end service independent of the network topology 
	- this is achieved by splitting messages into network sized packets and joining them back together agian at the other end 
	- often supports multiplexing to optimise network cost (several transport connections mapped into a single network connection) or splitting to enhance services (single transport to multiple connections)
- the session layer 
	- first upper layer crucial to internetworking 
	- manages the dialogue between end systems 
	- typically the session layer provides 
		- establishment and closing of connections 
		- synchronisation to allow checking and recovery of data 
		- negtiation of full and half duplex communication 
- the presentation layer 
	- provides a standard format for transferred information by overcoming compatability problems between systems using dissimilar data encoding rules and different display technologies 
- the application layer 
	- provides interface between application process
	- functions such as file transfer, remote job execution and application independent virtual terminal support are provided 
	- provides transparency to users, load balancing between machines, data bases, and the prospect of distributed operating systems 