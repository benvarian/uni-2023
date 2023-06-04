# Week 8 - Transport layer protocols and APIs

---
## port numbers 
- each arriving frame is further identified by a 16-bit positive port number that identifies the software end point to receive the payload 
- **one role of TCP is to demultiplexed each arriving segment to its corresponding communication end-point, using a port as an index**
- basically ports below 1024 are reserved for systems stuff and another above that are not reserved but can be already used by other applications 

## The transmission control protocol (TCP)
- transforms the raw IP into a full-duplex reliable character stream 
- uses sliding window with selective repeat protocol, and conveys a number of important fields in its TCP frame header 
- ![[Screenshot 2023-06-03 at 12.07.21 pm.png]]

### what tcp/ip provides to applications 
1. connection orientation 
	- making sure that one program must first request a connection to the destination before communication may proceed
2. reliable connection startup 
	- when two applications create a connection, both agree to the new connection so now old packets will interfere
3. point-to-point communication 
	- each communication session has exactly two endpoints 
4. full-duplex communication 
	- a single connection may be used for messages in both directions 
5. stream interface 
	- data is sent and received as a continuous sequence of bytes 
6. graceful connection shutdown 
	- TCP/IP guarantees to reliably deliver all pending data once a connection is closed by one of the endpoints 

### tcp/ip 3-way connection establishment and sequence numbers 
- a three-way handshale is employed in TCP's internal open sequnece 
- example 
	- if machine a wishes to establish a connection with machine b, a transmits the following message 
		- A->B: syn, $isn_a$ 
	- the initial request has the synchronise sequence number bit (ssn) set in its header and an initial 32-bit unsigned sequence number isn_a
	- B then replies with 
		- B->A: syn, isn_b, ack(isn_a)
	- to provide its own initial sequnce number, isn_b, and to acknowledge isn_a
	- a then acks isn_b with
		- a->b: ack(isn_b)

- ![[Screenshot 2023-06-03 at 12.16.14 pm.png]]


### tcp/ip retransmissions 
- basically theres such a big gap between potential hosts that it needs to cope with networks delays 
- it does this using the sliding window protocol, so timeouts are employed to force re-transmissions.
- to cope with this, tcp maintains a dynamic estimate of the current round trip time (RTT) for each connection. 
- as the round trip times vary, tcp averages round trip times into a smoothed round trip time that minimises the effects of usually long or short round trip times 
	- SRTT = (a x SRTT) + ((1-a) x RTT)
- a = smoothing factor, how much weight the new values are given 
	- when a = 1, the new value of the round trip time is ignored 
	- when a = 0, all previous values are ignored 
	- usually a is > 0.8 and < 0.9 
- **the smoothed round trip time estimates the average round trip time. to allow for queuing and transmission delays**
- tcp also calculates the mean deviation of the round trip time from the measrued value 
- SMDEV  = (a x SMDEV) + ((1-a) x MDEV) 
- RTO = SRTT + 2 $\times$  SMDEV

### tcp/ip congestion control 
- tcp attempts to avoid congestion collapse by using end-to-end packet loss as the metric of congestion 
- the tcp receiver normally fills the window field of an ack header to report how much additional buffer space is available for further data 
- when a message is lost tcp commences by sending a single packet. if an ack for this single packet returns, the sender next transmits two packets; if all of their acks return, up to four and so on
	- in effect, the protocol grows the senders sliding window until packets are lost, it then restarts at 1 
- tcp/ip responds by backing off, and avoids further congestion by slowly increasing offered traffic 

## network application program interfaces (apis)
- calls to open() return a file descriptor which is then used in calls to read() and write()

### berkeley sockets 
- the current socket implementation consists of three parts 
	- socket layer provides interface between user programs and the networking calls 
	- protocol layer supports different protocols in use 
	- device driver supports the physical devices such as ethernet controllers 

#### domain addressing 
- bascially there is different values that mean differnet types of addresses in a file called socket.h 
- this allows for an understanding on both sides of what type of request is required 

### establishing sockets with os system calls 
- the socket() establishes an end point of a communication link 
- third function call is usually 0 to indicate the default for the family/type combination 

### naming sockets
- when a socket is first made, it is unbound 
- and communication cant begin on an unbound socket, so yo use the bind() function to provide an address to the local end of the socket 
- you then use connect() to bind an address to the remote end of the socket 

#### connection establishment
- using listen() only indicates that an application is willing to accept requests, applications call accept() to accept them

### system call sequences 
- ![[Screenshot 2023-06-03 at 12.43.34 pm.png]]

---
# Week 9 - client/server design 

## What does a client process do?
- sends messages to a server process, requesting that the server performs a service 
- the client based process is the front end of the application that the user sees and interacts with 

## what does a server process do?
- receive requests from client programs 
- could be the host operating system or netwokr file server that provides file system services and application services 

## what is a two-tier architecture 
- where a client talks directly with a server
- used in small environments 

## three tier architecture 
- adds another server or agent between the clients and the traditional server
- the role of the agent is manyfold, can provide translation services, metering services (acting as a transaction monitor to limit the number of simultanenous requests to a given server)

## what is an intranet?
- the use of internet technologies for implementing internal client/server applications 
- one key advantage of web-based intranets is that the problem of managing code on the client is greatly reduced. assuming a standard browser on the desktop, all changes to the ui and functionality can nbe done by changing the code on the http server.
- second advantage is that if the corp already has the intranet setup, no additional code needs to be licensed or installed on client desktops. as to the user, internal and external information appears to be integrated 

## characteristics of client/server architectures 
- a combination of a client or front end portion that interacts with the users, and a server or back-end portion that interacts with the shared resource 
- front end and back end tasks have different requirements for computing resources 
- the environment is typically heterogeneous and multivendor 
	- the hardware platform and os of a client and server arent usually the same. so they communicate through a predefined set of standards 
- scalability 
	- horizontal scaling 
		- adding or removing clients with only a slight performance impact 
	- vertical scaling 
		- migrating to a larger and faster server 

## partitioning client/server responsibilities 
- in moving a single application to a seperated client/server config, must address some issues 
	- is there a functional partition at all
	- is there a data driven partition 
	- is there an extensive use of global variables 
	- are there any hidden intra-application communication mechanisms 

## concurrency in servers 
- motivation for concurrency in servers is speed 
- derived from using a non-queuing model of execution, either by using a new server to  support each client, or to provide faster time-sliced response to each client 
- if no concurrency is available in servers, the connections are blocked or refused 

- increased concurrency is required when 
	- forming responses requires significant i/o
	- processing time is proportional to the type of request 
	- high performance hardware is available 

- iterative servers - meaning a single request is handled at a time 
- concurrent servers - multiple requests at once


### iterative servers 
- server fully services each client until its completion 
- case 1 make clients wait 
	- if the time to service each client is lengthy, or of indeterminate duration, new clients may be kept waiting for their initial connection 
- case 2 - uses fork to handle each new client, thus there is no waiting involved 


## concurrent servers using select()
- can use select then specify the timeout time that will be sent to the client if nothing happens

## internet supervisor daemon - inetd
- main problem with having many inter networking services supported, is that each operating system host requires many daemons just waiting for incoming connections on their reserved port
- main solution is a single daemon, listening for incoming connections on many ports 
	- when a connection is made on say telnets port 23, the true telnet daemon is invoked to service the connection 


---

# Week 10 - Architecture independent applications 

## remote procedure call (RPC) paradigm
- based on the observation that procedure calls are a well understood mechanism for control transfer 
- proposal is that procedure calls may be consistently extended to access remote environments 
- when a remote procedure call is invoked 
	- the calling environment is suspended 
	- any parameters are passed across the network to the remote environment 
	- the required procedure is executed in the remote environment 
	- results are marshalled back to the caller and its execution resumes 

### rpc execution order 
- client calls a local procedure, 'client stub'
	- appears to the client that the stub is the actual server procedure that it wants to call
	- **purpose of the stub is to package up the arguments to the remote procedure, put them in some form and then build one or more network messages**
- network messages are sent to the local kernel using a system call
- network messages are sent to the remote kernel using either a connection based or connectionless protocol 
- server stub waits on the clients request
	- un-marshals the arguments from the network messages and possibly converts them to its own format
- server stub executes a local procedure call to invoke the actual server function 
- when the server procedure is finished it returns to the server stub, returning any required arguments 
- server stub converts the return values, and builds one or more network messages 
- messages will then traverse the network
- client stub reads the replies from the local kernel 
- after possibly converting the return values, the client stub returns to the calling procedure

## passing parameters to remote procedures 
- problems are introduced with parameter passing 
	- at worst, data types may need format conversion between machines. There exists a well defined data interchange standard, the external data representation (XDR) for transferring data between heterogeneous environments 
	- trouble happens when reference parameters must be passed. When local procedures are invoked a reference parameter such as a pointer may be passed and followed by the procedure

## naming and interface binding 
- when a sever boots it informs the database that it is alive and passes it 
	- programs program number 
	- programs version number 
	- port number 
- ![[Screenshot 2023-06-03 at 1.45.59 pm.png]]
	- the first time a client sub needs to locate a remote procedure it first asks the database server 
	- the server maps the procedures name to the network address 
	- **this process is called binding**

### locating and calling the server 
- when we start the server it creates a UDP socket and bind any local port to that socket. the function "svc_register" in the rpc library is called to register the server with the portmapper process. the portmapper keeps track of each server program number, verison number and port number 
- then start the client program which calls clnt_create. This function contacts the portmapper on the remote system to determine the UDP port number 
- client then calls the bin_date_1 function. the stub sends the call to the server stub using a udp datagram, integer is then returned as a single result 
- client then calls the str_date_1 function. the stub sends the single parameter to the server stub using a UDP datagram. the string result is returned in the parameter array 


## Semantics of remote procedure calls 
- make the function look like it manages local stuff the best you can 
- when a server crashes, the client stub may 
	- block and await the reply 
	- time-out and report a failure, or exception to the client 
	- time-out and retransmit the request 
- is important to understand whether a package supports a at-most-once or at-least-once semantics. Remote operations which may be repeated without consequence, **are termed idempotent operations**

## the external data representation 
- XDR is a standard for the description and encoding of data 
- **designed to provide the marshalling and un-marhsalling operations for Sun's implementation of RPC**
- xdr is also useful in situations which do not use RPC or even the network, as it allows one to read and write arbitrary c data structures in a consistent and well defined manner 

### differences in data representation 
- integers 
	- ![[Screenshot 2023-06-03 at 2.01.21 pm.png]]

## xdr approach 
- defines a standard xdr representation for data and makes it clients use it 
- a program receiving xdr information performs the opposite mapping, it converts the incoming xdr data to its own representation 

### xdr data representation 
- xdr assumes that bytes (octets) are portable between architectures 
- representation of all objects requires a mutliple of 4 bytes, numbered 0 to n-1
- the bytes are read from and written to streams such that byte m precedes byte m+1
- if the object being represented is not a multiple of 4 bytes in length then the n bytes are followed by enough 0 bytes to make the total byte count a multiple of 4 
	- consequence of this is that sending a single character will involved a 75% waste of bandwidth 
- xdr defines the representation of simple types, and the representation to be used when combining these types to produce more complex types 
- simply ttpyes 
	- ints 
	- floats 
	- chars 
	- enums and booleans 
- may be combined to produced complex types 
	- arrays 
	- strings 
	- structures 
	- discriminated unions 

--- 

# Week 11 - security of tcp/ip 

## Packet sniffing 
**- to capture information traversing the network is termed sniffing** 
- two probles with ethernets approach 
	- most ethernet nics can be placed in promiscuous mode, which means all observed packets being sent to the operating system 
	- most ethernet NICs permit their NIC address to be modified, programatically, and so one ethernet nic could be given the mac address of another 

- Packet sniffer
	- any hardware or software that can capture packets from the network, by setting a node's ethernet card to report all packets to the system/application regardless of the packets destination MAC address
- Network analysers 
	- monitor traffic and devices with the goal of alerting the network manager of problems 
- Protocol analysers 
	- capture network packets, provides a level of formatting for those packets, allowing the user to analyse/visualise packets post-hoc

Typical uses cases of programs 
	- sifting of clear text passwords and usernames 
	- conversion of data to human readable format so that people can read the traffic 
	- fault analysis to discover problems in the network 
	- network intrusion detection 
	- traffic logging 

## tcp/ip port scanning 
- using tools like nmap to see which ports are open for attacking 

## stealth port scanning 
- searching for open ports, but without creating a connection 
- half open scanning only performs the first part of TCP/IP handshake 
	- sends a syn flag and awaits a reply, a reply with the syn flag set reports an open port, with the rst flag set reports an inactive port. Half open scanning is favoured by potential attackers as nothing is logged 
- stealth determines a ports status by sending different combinations of tcp options 
	- send back a rst packet when they receive a FIN packet for a specified closed port 
	- send back a rst packet when they receive a fin/urg/push packet 
	- send back a rst packet for all tcp ports closed when they receive a packet without any ip flags set 


## Internet protocol (IP) spoofing 
- spoofing of ip packets allows an intruder on the internet to effectively impersonate a local systems IP address 
- ip spoofing and related attacks are possible because programs can open raw sockets, craete and send malformed ip packets 
- attacker uses source address spoofing for two reasons 
	- gain access to resources that only accept requests from specific source addresses 
	- hide the source of an attack by directing the blame at others 

## UDP packet spoofing 
- udp allows individual pakcets to be dropped 
- packets may be received in a different order then sent 
- applications using udp typically do not establish a protocol level session with their peers. each request and reply pair are often independent 
- an attacker may attack a udp service because of these properties 
- a poorly configured system may permit NFS-based files to be visible to external hosts. the attacker may then employ ip source spoofing over udp, to modify or delete a file 

## tcp/ip sequence number attacks 
- attacks exploit the non-randomness of the initial sequence numbers 
- the attacker c, establishes a valid connection with b, then determining one of b's current values for isn_b. the attacker c now impersonates a by sending a packet to b, but by setting a's nic address in the ethernet packet 
			- C(as a)->b: syn, isn_c
	- b then replies with 
		- b->a: syn, isn_b*, ack(isn_c)
	- to the true machine a, c will probably not see this message b->a, but can now guess the value of isn_b*. c now sends 
		- c(as a)->b: ack(isn_b*)
- now b believes that it has a valid connection with a. now a is confused as to why it is receiving b->a, it may either choose to ignore it or inform b with a reset packet that something is amiss 
- if a chooses to ignore the packet b->a, then c can continue to send packets to b, assuming a's identity. if c can see all replies from b->a in the session, then c can fully masquerade as a, while a ignores the transmission of which it is not a part


## denial of service attacks 
- uses source address spoofing, sends thousand of packets to a target system 
- stops legit users from using the systems has it becomes so slow 

## syn-flood attack 
- client sends a syn request to the server 
- server records the request on a queue of connections waiting to complete, replies with a syn/ack packet, and eagerly awaits the final ack reply 
- now the client doesnt send the ack reply, but sends thousands of syn requests with different source forged addresses
- to avoid syn-flood attacks, modern os will now employ large number of half-open sockets for new connections 
- now they will encode and ave the opening details as a 32-bit number, and use this as the initial sequence number in the syn/ack reply. only if the final ack reply returns will socket resources be allocated 

## distributed denial of service attacks 
- attacker will flood a single system with junk packets to consume bandwidth 
- using only a single attacker, the effect of the attack is greatly multiplied using attack servers termed agents, zombies, daemons and servers 
	- ![[Screenshot 2023-06-03 at 2.57.47 pm.png]]
- attacks are launched simultaneously from hundreds of remote controlled attack servers. the attacker must first gain access to the hundreds of agent machines
- single trojan program will sit on machine and wait for a simple udp or icmp packet to the agent 


## security at network boundaries 
- we wish to develop security practices at the boundary between a lan and the wider internet, to constrain the types of network traffic that may cross the boundary 
- we would like to 
	- control network traffic based on both senders and receivers network address
	- control network traffic based on requested services 
	- not expose our lan topology to the wider internet, hiding hostnames and so on

## packet filtering at network boundaries 
- use the term firewall to describe an network device, appliance which protects the boundary of an internal network 
- firewall is a software device through which all network packets must pass, both incoming and outgoing 
- end-runs 
	- a computer can access the internet without passing its traffic through the firewall 
- traffic tunneling 
	- users or applications can embed certain types of unwanted network traffic within permitted protocols 

## possible packet filtering criteria 
- network packets may be filtered on a number of criteria 
- by examining the headers of tcp/ip traffic you can detect bad traffic
	- filter on each ip packets source address
		- packets that announce their source address as being from an internal network will probably have a spoofed address
	- filter on each ip packets destination address 
		- packets destined for an internal network address should not leave the network via an external interface
	- based on specific low-level routing or transport protocols 
		- denying all icmp or udp traffic from leaving 
	- based on application protocols 
		- permitting http and ftp rquests to leave but not nfs requests 
	- based on recent activity 
		- stateful filtering has knowledg of recent traffic 


## develop a firewall policy 
- a consistent and consistently applied policy is a strong argument by system admins to deny individual requests for new small holes in the firewall by individuals 


## packet filtering with iptables 
- two software components 
	- application program, controlling the set of rules and policies to be enforced 
	- netfilter software configured as part of an operating system kernel 

## ip masquerading 
- technique employed within a firewall, to translate or map one set of ip addresses to another 
- to use NAT, the firewall connecting the internal LAN to the external internet will have at least two network cards each with their own ip addresses 
- primary motivations for nat are 
	- the isp may only provide one ip addres to use, nat permits multiple hosts to use the same ip address
	- simplifies the later growth and re-design of a network 
	- external attackers cannot easily learn the topology of your internal network unless they penetrate your firewall

## Network address translation (nat)
- overloaded nat 
	- maps multiple unroutable ip addresses to a single registered ip address by using different ports 
- dynamic nat
	- maps an unroutable ip address to one of a managed group of registered ip addresses
- static nat 
	- maps an unroutable ip address to a registered ip address on a one-to-one basis 
	- required when a device needs to be accessible form outside the networ such as a web or ftp server

## connection tracking 
- the ability for a firewall to maintain state information about connections 
- firewalls that are able to do this are termed stateful.
- considered more powerful then non sateful 


---

# Week 12 - Cryptography's role in networking 

## the iso/osi security architecture 
- the iso/osi group has a range of terminologies forming their iso/osi security architecture 
- includes 
	- data confidentiality 
		- protecs data as it traverses the network from being disclosed to the incorrect parties 
	- data integrity 
		- protects the data from modification or removal
	- data origin authentication 
		- validates the senders data 
	- data receiver authentication 
		- validates the receiver of the data 
	- peer-entity authentication 
		- validates all network components
	- non-repudiation 
		- creates and verifies evidence that the claimed sender sent the data, that the intended receiver did receive it, and that neither can deny that this occurred 

## cryptographys role in networking 
- we assume that an adversary is able to 
	- copy data from disk storage for remote analysis 
	- passively listen on broadcast channels 
	- aggressively monitor traffic through intermediate routers or workstations 
	- actively replay, modify or insert their own messages into the stream 

## basic cryptographic terminology 
- encryption function and a key to convert the plaintext (input) into ciphertext (output)
- assume that the adversary knows the encryption method been used, and that the key is secret and changed frequently 
- different ypes of attacks 
	- plaintext attack
		- the attacker has a block of plaintext and its corresponding block of ciphertext.
	- chosen plaintext attack
		- the attacker can have their victim encrypt fixed, known blocks of data 
	- differential analysis 
		- many similar plaintexts being encrypted, and the result being compared 


## influence of computers on cryptography 
- an algorithm's strength is not simply derived from its key length, but from its peer evaluation and public review 
- a weak algorithm is that whose implementation isn't available, and its strength would be compromised if those details where to be made public 

## symmetric cyhpers 
- the data encryption standard (des), is a symmetric cipher, private key algorithm, **in which the sender and receiver use the same key that must be kept private** 

## des algorithm 
- des software is publicly available
- data is encrypted in 64 bit blocks 
- ciphertext is output in 64 bit blocks 
- 56 bit key is used 
- same key is then used for both encryption and decryption 

### steps of the des algorithm 
- step 1 transpositon of plaintext
- step 19 inverse of above 
- step 18 exchange left 32 bits with right 32 bits 
- steps 2-17, use a function of the key for each stage, which we shall call K_i

- ![[Screenshot 2023-06-04 at 11.30.02 am.png]]

## triple DES
- des still in use today in what is called 3des 
- where des only uses one 56 bit key, 3des uses 3 56bit keys in order to make it harder to crack 

## des modes - eletronic code book (ecb)
- each block of ciphertext is independent of other blocks and is most frequently used for the coding of data on some storage medium 
	- ![[Screenshot 2023-06-04 at 11.34.12 am.png]]

### des modes - cipher block chaining (cbc)
- **chaining ensures that each block is dependent on earlier blocks**
	- ![[Screenshot 2023-06-04 at 11.34.48 am.png]]
- now an attacker wont be able to alter anything without it being obvious that something has changed 


## exchanging of encryption keys 
- simple anaology of how keys can be exchanged 
	- a wants to send a key to b
	- a puts the key in a secure box and locks it with a's padlock
	- b does not have the key to a's padlock 
	- b receives the box and adds b's own packlock to the box and returns it to a
	- a removes a's padlock with a's own key and sends the box back to b
	- b can now remove b's own padlock and remove th ekey which is now shared between a and b

## public key cryptography 
- public key, e, which is openly published 
- private key, d, which is known only by recipient 

steps 
- a and b openly publish their public keys $E_A$ $E_B$ 
- a sends $E_b$(plaintext) to B
- B calculates $D_B$($E_B$ (Plaintext)) = plaintext
- b can then reply with $E_A$(plaintext) for a to read


## rsa algorithm 
- ![[Screenshot 2023-06-04 at 11.40.48 am.png]]
- chose 2 very large prime numbers, p and q, each over 100 digits 
- define E_a to be the pair (e,n) where n = pxq
- define D_a to be the pair (d,n) where (e x d) mod ((p-1) x (q-1)) = 1

- then use 
	- encryption function 
		- C := P_e mod n 
	- decryption function 
		- P := C_d mod n 

## strong encryption is not enough (digital signature)
- unlike traditional signatures, a digital signature cannot be a constant, it must be a function of the document that it signs 
- prevents two types of fraud 
	- forging of a signature by the receiver 
	- repudiation of the transmission of a message by the sender 

- two categories of a digital signature are identified 
	- true signatures, signed by the sender, verified by the receiver 
	- arbitrated signatures, only send and verified through a trusted third party 

## message digests 
- central to digital signatures 
- when a message is signed, its contents are first hashed to give a message digest
	- the digest is then encrypted with the senders secret key, giving a proof of the senders identity 

- a good digest must 
	- have an absence of collisions 
		- must be hard to find two messages with the same digest 
	- not be invertible 
	- have a uniform distribution of results 
		- a change in just one bit should affect at least half the ouput bits 

- some popular message digests 
	- md2 and md5 
	- sha-1, sha-2, sha-256


## digital signature generation 
- a digital signature is a summary of the original message, but also provides an assurance that the creator has the private key that matches the public key used to generate the signature 
- ![[Screenshot 2023-06-04 at 11.56.30 am.png]]


## digital certificates 
- "drivers license for the internet"
- **provides a binding between an entity public key, and one or more attributes to its identity**

- an entity may be a person, a execution piece of software, or a device such as a router 
- certification authority (CA) attests to the authenticity of the entitys public key by digitally signing a message with its own private key 
- quality of the certificate depends on the detail of information provided to the CA
- either public and private keys may be issued by the CA, or the CA may challenge the entitys public key 


### digital certificate encoding 
- data is encoded using abstract syntax notation 

## certificate path validation 
- CAs are organised in hierarchies, each parent CA signs a certificate vouching for a subordinate CA's public key 
- when validating a chain of certificates, the certificate path is followed until the top of the chain is reached 
- ![[Screenshot 2023-06-04 at 12.04.35 pm.png]]

## certificate revocation list 
- allows clients and servers to check whether the entity they are dealing with has a valid certificate 
- trust breaks down, and crls are requried when 
	- a subjects private key is exposed 
	- ca's private key is exposed 
	- relationship between the subject and ca changes 
- certificate revocation 
	- obtain the subjects digital certificate and verify its validity 
	- extract the serial number of the certificate 
	- fetch the current crl from the ca 
	- verify the crl's digital signature, and record its publication time and when the next crl is to be publihed 
	- look at the crl to determine if the intended certification has been revoked or suspended 
	- alter the user if the certificate has been revoked 