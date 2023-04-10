## 3.3 elementart data link protocols 

### 3.3.1 initial simplyfying assumptions 
- independent processes
	- to start with we assume that the physical, data link and network layer and independent processes that communicate by passing messages back and forth
- undirectional communication 
	- that machine A wants to send a long stream of data to machine B, using a reliable, connection oriented service 
	- A is assume to have an infinite supply of data ready to send and never has to wait for data to be produced. instead when A's data link layer asks for data, the network layer is always able to comply immediately 
- reliable machines and processes 
	- assume that machines dont crash 
	- these protocols deal with communication errors, but not the problems caused by computers crashing and rebooting 
	- as far as the data link layer is concerened, the packets passed across the interface to it from the network layer is pure data, whose every bit is to be delivered to the destinations network layer. 

### 3.2.2 basic transmission and receipt 
- when the data link layer accepts a packet from the network layer at the sender, it encapsulates the packet in a frame by adding a data link header and trailer to it
- thus a frame consits of an embedded packets, some control information and a checksum
- initially the reciever has nothing to do, in this example we will indicate that the data link layer is waiting for something to happen by the procedure call waitforevent(&event). this proceduer only returns when something happened. the set of possible events differs for the various protocols to be described and will be defined seperately for each protocol
- when a frame arrives at the receiver, the receiver computes the checksum. if the checksum in the frame is incorrect, the data link layer is informed (event = cksum_err). if the inbound frame arrived undamaged, the data link layer is also informed (event=frame_arrival) so that it can aquire the frame for inspection using from_physical_layer. as soon as the receiving data link layer has acquired an undamaged frame, it checks the control information in the header and if everything if all right, passes the packet portion to the network layer 
- a frame has 4 fields, kind, seq, ack and info, the first 3 contain information and the last of which may contain actual data to be transferred. these control fields are collectively called the **frame header**. 
- ![[Screenshot 2023-04-10 at 1.18.31 pm.png]]
- the *kind* fields tells whether there is any data in the frame. 
- the *seq* and *ack* fields are used for sequence numbers and acknowledgements.
- the *info* field of a frame contains a single packet, the info field of a control frame isnt used, a more realistic implementation would use a variable length info field omitting it altogether for control frames 
- the network layer buils a packet by taking a message from the transport layer and adding the network layer header to it. this packet is then passed to the data link layer for inclusion in the info field in the outgoing frame 
- when the frame arrives at the destination, the data link layer extracts the packet from the frame and passes the packet to the network layer.
- in most of the protocols, we assume that the channel is unreliable and loses entire frames upon occasion. to be able to recover from such calamities, the sending data link layer must start and internal timer or clock whenever it sends a frame. if no reply has been recived within a certain predetermined time interval, the clock times out and the data link layer recives an interrupt singal 
- this is handlded by allowing the procedure waitforevent to return event = timeout, the procedures starttimer and stoptimer turn the timer on and off. 
- the procedures startacktimer and stop control an auxiliart timer used to generate acknowledgements under certain conditions 
- the procedures enable and disable networklayer are used in more sophisticated protocols, where we no longer assume that the network layer always has packets to send. when the data link layer enables the network layer, the network layer is then permitted to interrupt when it has a packet to be sent. we indicate this by event=network_layer_ready. by being carefuly about when it enables and disables its network layer, the data link layer can prevent the network layer from swapping it with packets for which it has no buffer space. 

### 3.3.3 simplex link layer protocols 
- utopia no flow control or error correction 
	- data is only transmitted in one direction only 
	- both the transmitting and receiving network layer are always ready 
	- processing times can be ignored 
	- infinited buffer space is available 
	- the communication channel between the data link layers never damages or loses frames 
- **adding flow control stop and wait** 
	- now the problem of preventing the sender from flooding the receiver with frames faster than the latter is able to process them 
	- allow the receiver to provide feedback to the sender 
	- after having passed a packet to its network layer, the receiver sends a little dummy frame back to the sender which, in effect, gives the sender permission to send the next frame.
	- after having sent a frame, the sender is required by the protocol to bide its time until the little dummy frame arrives. 
	- ![[Screenshot 2023-04-10 at 2.00.09 pm.png]]
- **adding error correction: sequence number and ARQ**
	- lets consider the situation of a communication channel that makes errors 
	- frames may either be damaged or lost completly 
	- assume that if a frame is damaged in transit, the receiver will detect this when it computes the checksum. 
	- **if the frame is damaged in such a way that the checksum is nevertheless correct, this protocol and all others can fail**
	- both sender and receiver have a variable whose value is remembered while the data link layer is in the wait state 
	- the sender remembers the sequence number of the next frame to send in nextframetosend(), the receiver remembers the sequence number of the next frame expected in frameexpected().
	- **after transmitting a frame, the sender starts the timer running. if it was already running, it will be reset to allow another full timer internval. the interval should be chosen to allow enough time for the frame to get to the receiver, for the receiver to processs it in the worst case and for the acknowledgment frame to propagate back to the sender.** 
	- only when that interval has elapsed it is safe to asume that either the transmitted frame or its acknowledgemnt has been lost and to send a duplicate.
	- if the timeout interval is to short, the sender will transmit unnecessary frames.
	- after transmitting a frame and starting the timer, the sender waits for something to happen. only 3 possibilites exist 
		- an acknowledgement frame arrives undamaged
		- a damaged acknowledgement frame staggers in
		- or the timers expires
	- if a valid acknowledgement comes in, the sender fetches the next packet from its network layer and puts it in the buffer, overwriting the previous packet. also advances the sequence number 
	- if a damaged frame arrives or the timer expires, neither the buffer nor the sequence number is changed so that a duplicate can be sent. in all cases the contents of the buffer are then sent 
	- when a valid frame arrives at the reciver, its sequence number is checked to see if it is a duplicate. if it isnt, it is accepted then passed onto the network layer, and an acknowledgement is generated. 
	- duplicates and damaged frames are not passed to the network layer, but they do cause the last correctly received frame to be acknowledged to signal the sender to advance the next frame or retransmit a damaged frame. 

## 3.4 improving efficiency 
- piggybakcing that can help a link layer protocol acheive bidriectional transmission, and a concept called a sliding window that can improve transmission effeiciency by allowing the sender to have multiple bytes in flight 

### bidirectional transmssion: piggybacking 
- use the same link for data in both directions. in this model the data frames from A to B are intermixed with the acknowledgement frames from A to B. by looking at the kind field in the header of an incoming frame, the reciver can tell whether the frame is data or an acknowledgement.
- when a data frame arrives, instead of immediately sending a seperate control frame, the receiver restrains itself and waits until the network layer passes it the next packet. the ack is attached to the outgoing data frame. 
- in effect, the ack gets a free ride on the next outgoing data frame. 
- the technique of temporarily delaying outoging acknowledgements so that they can be hooked onto the next outgoing data frame is known as piggybacking. 
- the main advantage of using this is a better use of the available channel bandwidth
- the ack field in the frame header costs only a few bits, whereas a seperate frame would need a header, the ack, and a checksum. 
- in addition, fewer frames sent generally means a lighter processing load at the receiver 
- **piggybacking downsides** 
	- how long should the data link layer wait for a packet onto which the piggyback acknowledgement?
		- if the data link layer waits longer than the senders timout period, the frame will be retransmitted, defeating the whole purpose of having acks.
		- **must resort to some adhoc scheme, such as waiting for a fixed number of milliseconds. if a new packet arrives quickly, the ack is piggybackd onto it. otherwise if no new packet has arrived by the end of this time period, the data link layer just sends a seperate ack frame**

### sliding windows 
- in these protocols, each outbound frame contains a sequence number, ranging from 0 up to some maximum. the max is usually $2^n - 1$ so the sequnece number fits exactly in an n-bit field. the stop and wait sliding window protocol uses n=1, restricting the sequence numbers to 0 and 1, but more sophisticated version can use an arbitrary n.
- **the essence of all sliding window protocols is that at any instant of time, the sender maintains a set of sequence numbers corresponding to frames it is permitted to send. these frames are said to fall within the sending window.**
- similarly, the receiver also maintains a receiving window corresponding to the set of frames it is permitted to accept. the senders window and the recivers window dont need the same upper and lower limits or even the same size. 
- since frames currrently within the senders windows may be lost or damaged, the sender must keep all of these frames in its memory for possible retransmission. Thus if the maximum window size is n, the sender needs n buffers to hold the unack frames.
- if the window ever grows to its maximum size, the sending data link layer must forcibly shut off the network layer until another buffer becomes free.
- the receiving data link layers window corresponds to the frames it may accept. any frame falling within the window is put in the receviers buffer. When a frame whose seq number is = to the lower edge of the window is received, its passed to the network layer and the window is rotated by one. any frame falling outside the window is discarded. in all of these cases a subsequent ack is generated so that the sender may work out how to proceed. 

## 3.4.2 example of full-duplex, sliding window protocols 

### one bit sliding window 
- window size of 1 meaning only 1 bit of data is allowed to be in transit at any given time.
- the sender can transmit only one bit of data at a time. after sending a bit of data, the sender waits for an ack from the receiver. 
- if the sender does not receive an ack within a specified time frame, it assume that the data was lost or corrupted and resends the bit. this process then continues until the receiver sends an ack, indicating that all the data has been received correctly. 
- once the sender receives an ack, it can send the next bit of data. the receiver maintains a buffer to store the received data until all the data has been received. once all that data has been received, the receiver sends a final ack to the sender, indicating that the transmission is complete. 
- simple but inneficient since it can lead to a significant amount of retransmissions and can cause delays in data transfer. 

### go-back-n
- allowed to transmit multiple packets up to a certain window size, before receiving an ack from the receiver. 
- the sender maintains a buffer to store the sent packets until an ack is received. the receiver has a buffer to store the received packets until they are delivered to the upper layer of the protocol stack
- uses a sequence number for each packet, which is incremented for each packet that is sent. the receiver then sends an ack for each received packet, indicating the sequence number of the next expected packet. if the receiver receives a pacekt with a sequence number that is out of order, it discards the pacekt and does not send an ack until it receives the expected packet. 
- if the sender doesnt receive an ack frame for a packet within a specified time frame, it assume that the pacekt was lost or corrupted and retransmits all the pacekts from the lost packet onwards.
- this is what is referred to as the go-back-n operation. where the sender goes back to the last acknowledged packet and retransmits all the packets after that packet. **this ensures that all pacekts are received in order and no packets are lost**
- the window size determines the max number of packets that can be sent before receiving an ack. 
- if the window size is to small the protocol may not utilise the availble network bandwith efficiently.
- if the window size if to big, the protoocl may experience congestion and result in packet loss 
- **is a reliable and efficient protocol for data transfer in computer networks. it is commonly used in situations where there is a high probability of packet loss**

### selective repeat 
- unlike go-back-n, selective repeat allows the sender to retransmit only the lost or corrupted packets, rather than all the packets from the last ack packet. 
- when the sender receives a negative ack or a timeout for a particular pacekt, it retransmits only that pacekt and waits for an ack. 
- the sender can send multiple packets within the window size, and the receiver can acknowledge each pacekt individually, allowing for a more effective use of network resources. 
- commonly used in situations where there is a low probability of packet loss and where network resources are limited