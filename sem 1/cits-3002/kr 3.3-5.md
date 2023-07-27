## connectionless transport: udp
- udp takes messages from the application process, attaches source and destination port number fileds for the multipliexing/demultiplexing service, adds two other small fields, and passes the resulting segment to the network layer
- network layer encapsulates the transport layer segment into an IP datagram, then makes an attempt to deliver the segment to the receiving host 
- if the segment arrives at the receiving host, udp uses the destination port number to deliver the segments data to the correct application process

- when a DNS application wants to make a query, it constructs a dns message and passes it to UDP
- with no handshaking, the host side udp adds header fields and passing the resulting segment to the network layer 
- network layer puts the udp segment into a datagram and send it to the server 
- the dns application on the querying side then waits, if it doesnt receive anything, it might try resending the query, try sending to another server, or informing the application that made that request that there was a failure 

advantages of using udp over tcp 
- finer control over what data is sent and when 
- no connection establishment 
	- basically using tcp for things that dont need it only slows things down, so using udp for things like dns is the right call, but using tcp for things like webpage is much more important 
- no connection state 
	- as tcp maintains connection state between machines things can become slow with the more hosts that are connected
	- whereas udp doesnt so a server thats devoted to a particular purpose can usually support many more clients 
- small packet overhead 
	- tcp has 20 bytes of overhead 
	- udp has 8 bytes

### udp segment structure 
- refer to drawing 
- source port, dest port, length, checksum and message 
- the reason udp does its own checksum stuff is due to the unreliability that all links between source and dest provide its own form of error checking 

## reliable data transfer 
- responsiblity of a reliable data transfer protocol to implement service abstraction 
- if a sender is willing to wait long enough to know that a packet didnt reach its destination, it can retransmit it 
- duplicate data packets 
	- when a sender waits so long to know if the pakcet reached its final destination that it sends out another one even though it mightve received the packet 
- countdown timers
	- iterrupt the sender after a given amount of time has expired 

- pipelining 
	- so usually u send p1 then wait for ack, but instead you send p1 -> p2 and so on without waiting for ack until you get to like p4, then make sure you receive 4 acks basically 
	- consequences 
		- range of sequcne numbers must be increased 
		- sender and receiver sides may have to buffer more than one packet 

#### go-back-n
- allowed to send multiple packets without waitinf for ack, but is constrained to no more than the max number, n, of unknown acks in the pipeline
- n is referred to as the window size 
- and often refered to as the sliding window protoicol

- ![[Screenshot 2023-06-05 at 1.08.24 pm.png]]


#### selective repeat 
- having sender retransmit only those packets it suspects were received in error at the receiver 
- requires sender ack each packet that is correctly received 
- send_base is basically the first/last packet that hasnt received an ack yet so that is say 0, then when say the ack for 0 is received is can move to say 3 which is yet to receive an ack so that becomes 0 
- ![[Screenshot 2023-06-05 at 1.13.44 pm.png]]

## connection oriented transport: TCP 
- intialises with a handshake 
- provides a full-duplex service 
	- if theres a tcp connection between process a on one host and process b on another host, then application layer data can flow from a to b at the same time 
- always point-to-point 
	- communication is between a single sender and a receiver
- sequence number for a segment is therefore the byte-stream number of the first byte in the segment

## Round trip time esitmation 
estimatedRTT = (1- a) x EstimatedRTT + a x SampleRtt

- selective acknowledgement 
	- allows a tcp receiver to ack out-of-order segments selectively rather than just cumulatively ack the last correclty received 
- congestive control
	- tcp things have a variable that provides a num on the flow rate  which is called the receive window. This is used to give the sender an idea of how much free buffer space is available at the receiver 