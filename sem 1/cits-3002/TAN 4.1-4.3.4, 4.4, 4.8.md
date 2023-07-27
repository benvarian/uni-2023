
## 4.1 the channel allocation problem 
- how to allocate a single broadcast channel among compteing users 

### 4.1.1 static channel allocation 
- each device or user is assigned a specific channel for communication, and the channel remains fixed unless the system is reconfigured 
- used in systems that have a small number of users or devices and a relatively stable traffic pattern like telephone networks, cable television networks 
- if there are N users, the bandwith is divided into N equal sized portions, with each users being assigned one portion. since each user now has a private frequency band, there should be no interference among users.
- each channel has a fixed capacity, and the total capacity of the system is determined by the number and capacity of the channels. the capacity of each channel is determined by the modulation technique used, the bandwith available and many other factors 
- main advantage is that its simply and easy to implement. 
	- channels are assigned in advance, no dynamic reconfiguration is required during operation
- limitations 
	- since the channels are assigned in advance they may not be used efficiently if the traffic patterns change or if some devices or suers require more capacity than others 
	- can lead to underutilisation of some channels and congestion on others 

### 4.1.2 assumptions for dynamic channel allocation 
- independent traffic 
	- the model consists of N independent stations, each with a program or user that generated frames for transmission 
	- the expected number of frames generated in an interval of length $\Delta$t and $\lambda$$\Delta$t, where $\lambda$ is a constant (the arrival rate of new frames).
	- once a frame has been generated, the station is blocked and does nothing until the frame has been successfully transmitted 
- single channel 
	- a single channel is available for all communcation
	- all stations can transmit on it and can receive from it 
	- the stations are assumed to be equally capable, though protocols may assign them different roles 
- observable collisions 
	- if two frames are transmitted simultaneously, they overlap in time and the resulting signal is garbled 
	- this event is called a collision 
	- all stations can detect that a collision has occured.
	- a collided frame must be transmitted again later 
- continuous or slotted time 
	- time may be assumed continuous, in which case frame transmission can begin at any instant.
	- Frame transmissions must then begin at the start of a slot
- carrier sense or no carrier sense 
	- stations can tell if the channel is in use before trying to use it 
	- if there is no carrier sense, stations cannot sense the channel before trying to use it. they just go ahead and transmit

## 4.2 multiple access protocols 

### 4.2.1 aloha 
- pure aloha 
	- basic idea of aloha 
		- let users transmit whenever they have data to be sent
		- there will be collisions, and the colliding frames will be damaged 
	- after each station has sent its frame to the central computer, this computer rebroadcasts the frame to all of the stations.
	- a sending station can thus listen for the broadcast form the hub to see if its frame has gotten through
	- if the frame was destryoed the sender just waits a random amount of time and sends it again. the waiting time must be random or the same frames will collide over and over. 
	- if the first bit of a new frame overalps with the last bit of a frame that has almost finished, both frames will be totall destroyed and both will have to be retransmitted later 
- slotted aloha 
	- the time is divided into discrete slots
	- the devices are synchronised to these slots, and each device can transmit in a single slot 
	- if a device has data to transmit, it waits until a new slot opens 
	- if the transmission is a success the device is informed 
	- if the trnamssion is unsuccessfuly the device will wait for a random amoint of time and tries again in the next slot 
	- main limitation 
		- the maximum channel utilisation is limited to 37%, which means that only 37% of the total slots can be used for successful transmission 

### 4.2.2 carrier sense multiple access protocols 
- persistent and nonpersistent CSMA 
	- 1 persistent
		- when a station has data to send, it first listens to the channel to see if anyone else is transmitting at that moment. 
		- if the channel is idle, send data 
		- if the channel is busy, the station waits until it becomes idle 
		- then the station transmits a frame
		- if a collision occurs the sation waits a random amount of time and starts all over again 
		- this type of protocol is called 1-persistent as the station transmits with a probability of 1 when it find the channel idle 
	- non-persistent 
		- concious attempt is made to be less greedy than in the previous option 
		- as before a station sense the channel when it wants to send a frame, and if no one else is sending, the statoin begins doing so itself immediately 
		- however, if the channel is already in use, the station does not continually sense it for the purpose of seizing it immediately upon detecting the end of the previous transmission. 
		- **instead it waits a random time period and then repeats the algorithm**
	- p-persistent 
		- applied to slotted channels 
		- when a station becomes ready to send, it senses the channel
		- if its idle, it transits with a probability p
		- with a probability q = 1 - p, it defers until the next slot 
		- if that slot is also idle, it either transmits or defers again, with probabilities p and q. this process is repeated until either frame has been transiteed or another station has begun transmitting 

- CSMA with collision detection 
	- allows the stations to quicly detect the collision and abruptly stop transmitting sicne they are irretievably garbled anyway. this strategy saves time and bandwith 
	- stations hardware must listen to the channel while it is transmitting 
	- if the signal it reads back is different from the signal it is putting out, it knows that a collision is occuring 
	- contention algorithm
		- suppose that two stations both begin transmitting at exactly the same time $t_0$. 
		- the minimum time to detect the collision is jsut the time it takes the singal to propagate from one station to the other.
		- consider the worst case scenario, let the time for a singal to propagate between the two farthest stations be r. at $t_0$ one station begins transmitting. at $t_0$ + r - e, an instant before the signal arrives at the most distant station, that station also begins transmitting.
			- of course itll detect the collision almost instantly and stops, but the little noise burst cause by the collision does not get back to the original station until time 2r-e. 
			- in other words the worst case a station cannot be sure that it has seixed the channel until it has transmitted for 2r without hearing a collision. 

---
### 4.2.3 collision free protocols 
- bit map protocol
	- each contention periods consists of exactly N slots 
	- if station 0 has a frame to send, it transmits a 1 bit during the slot 0. 
	- no other station is allowed to transmit during this slot 
	- regardless of what station 0 does, station 1 gets the oppourtunity to transmit a 1 bit during slot 1, but only if the frame is queued
	- **in general, station j may announce that it has a frame to send by inserting a 1 bit into slot j. after all N slots have been passed by, each station has complete knowledege of which stations wish to transmit.**
	- a file is broken down into smaller pieces and then distributed amongst the users on the peer-to-peer network. each user who then downloads a peice of that file becomes a host for that piece and can then share it with the other users on that network
	- the status of each file is represented by a bitmap, each value will represent the status of a specific piece of the file, indicating if its been downloaded, currently been downloaed or if its still available for download 
	- when a user requests a piece of the file, the bitmap is use to determine which other users have that piece available for sharing. 
- token passing 
	- the essence of the bit-map protocol is that it lets every station transmit a frame in turn in a predefined order.
	- another way to accomplish the same thing is to pass a small message called a token from one station to the next in the same predefined order. 
	- The token represents the permission to send.
	- if a station has a frame queed for transmission when it receives the token, it can send that frame before it pases the token to the next station 
	- if there is no queued frame, it simply passes the token 
	- in a token ring protocol, the topology of the network is used to define the order in which stations send. The stations are connected one to the next in a single ring. Passing the token to the next station 
	- ![[Screenshot 2023-04-11 at 10.59.39 am.png]]
	- the protocol is called token bus 

- binary countdown 
	- a station wanting to use the channel now broadcasts its address as a binary bit string, starting with the high-order bit. 
	- the bits in each address position from different stations are boolean ORed together by the channel when they are sent at the same time 
	- how it works 
		- for example if stations 0010, 0100, 1001, and 1010 are all trying to get the channel 
		- in the first bit frame the station trasmit 0,0,1,1 
		- these are ORed together to form a 1
		- stations 0010 and 0100 see the 1 and know that a high numbered station is competing for the channel, so they give up for the current round
		- stations 1001 and 1010 continue 
		- the next bit is then 0, both stations continue
		- the next bit is 1 so station 1001 gives up 
		- and 1010 gets it 
		- after winning the bidding, it may now transmit a frame after which a whole nother bidding cycle will commence 

### 4.2.4 limited contention protocols
- adaptive tree walk protocol 
	- in the first contention slot following a successful frame transmission, slot 0, all stations are permitted to try to acquire the channel 
	- if there is a collision, the during slot 1 only those stations falling under node 2 in the tree may compete. 
	- if one of them acquires the channel, the slot following the frame is reserved for those stations under node 3
	- if on the other hand two or more stations under node 2 want to transmit, there will be a collision during slot 1, in which case it is node 4s turn during slot 2 

### 4.2.5 wireless lan protocols 
- a early and influential protocls that tackles these problems for wireless LANs is MACA (Multiple access with collisions avoidance)
	- the idea is for the sender to stimulate the receiver into outputting a short frame, so stations nearby can detect this transmission and avoid transmitting for the duration of the upcoming large data frame 
	- ![[Screenshot 2023-04-11 at 11.13.55 am.png]]

## 4.3 ethernet 

### 4.3.1 classical ethernet pyhsical layer 

### 4.3.2 classic ethernet MAC sublayer protocol
- first comes a preamble of 8 bytes, each containing the bit pattern 10101010.
- the last byte is called the start of frame delimeter 
- the manchester encoding of this pattern produces a 1-Mhz square wave for 6.4 usec to allow the receivers clock to synchronise with the senders 
- the last two 1 bits tell the receiver that the rest of the frame is about to start 
- ![[Screenshot 2023-04-11 at 11.20.11 am.png]]
- next comes two addresses, one for the destination and one for the source 
- each 6 bytes long 
- the first transmitted bit of the destination address is a 0 for ordinary adresses and a 1 for group addresses 
- group addresses allow for multiple stations to listen to a single address. when a frame is sent to a group all the stations receive it. called multi-casting 
- a frame containing all 1s in the destination field is accepted by all stations on the network 
- next comes the type or length field, to tell the receiver what to do with the frame. specifies which processs to give the frame to, for example a type code of 0x0800 means that the data contains an IPv4 packet.
- the receiver doesnt know what to do with an incoming frame so it added another header for the lgoical link control protocol within the data. uses 8 bytes to convey the 2 bytes of protocol type information 
- CSMA/CD with binary exponential backoff 
	- classic ethernet uses the 1-persistent CSMA/CD algorithm, means that stations sense the medium when they have a frame to send and send the frame as soon as the medium becomes idle, if theres a collision they abort the transmission with a short jam signal and retransmit after a random interval 
	- if there is no collision, the sender assumes that the frame was probably successfuly delivered, as neither CSMA/CD or ethernet provides acks. this is because its appropriate for wired and optical fibre channels that have low error rates 

### 4.3.4 switched ethernet  
- the wires were telephone company twisted pairs
- adding or removing a station is simpler in this configuration, and cable breaks can be detected easily 
- with the advantages of being able to use exisitng wiring and ease of maintenance, twisted pair hubs quickly became the dominant form of ethernet 
- **the heart of this system is a swtich containing high-speed backplane that connects all of the ports.**
- a switch has the same advantages as a hub too. it is easy to add or remove a new statoin by plugging or unplugging a wire, and it is easy to find most faults since a flaky cable or port will usually affect just one station.
- switches only ouput frames to the ports for which those frames are desitned. when a swtich port recives an ethernet frame from a statoin, the switch checks the ethernet addresses to see whcih port the frame is destined for 
- a switch improves performance over a hub in two ways 
	- no collisions
	- with a swtich multiple frames can be sent simultaneously 
		- these frames will reach the switch ports and travel over the swtichs backplane to be output to the proper prots. 
		- however, since two frames might be sent to the same output port at the same time, the switch must have buffering so that it can temporarily queue an input frame until it can be transmitted to the output port 

## 4.4 wireless lans 
### 4.4.1 the 802.11 architecture and protocol stack 
- can be used in two modes 
	- to connect clients to another another network 
	- an ad hoc network
		- a colllection of computers that are assoicated so that they can directly send frames to each other.
		- no internet access

### 4.4.2 the 802.11 physical layer 
- all of the 802.11 techniques use short-range radios to transmit signals in either the 2.4ghz or 5ghz frequency bands 
- the idea is that different rates can be used depending on the current conditions 
	- if the wireless signal is weak, a low rate can be used. if the singal is clear, the highest rate can be used. 
	- this is called rate adaption 
- 802.11b 
	- a spread-spectrum method that supports rates of 1,2,5.5,11 mbps. 
	- only one spreading code that is shared by all users. spreading is used to satisfy the FCC requirement that power be spread over the ism band. 
	- the spreading sequence used by 802.11b is called Barker sequence. 
		- its autocorrelation is low excep when the sequences are aligned. This property allows a receiver to lock onto the start of a transmission, 
- 802.11a 
	- supports up to 54bps in the 5ghz band.
	- based on OFDM (ortogonal frequency division multiplexing), because OFDM uses the spectrum efficiently and resits wireless signal degradations such as multipath 
	- 802.11b has a range that is about 7 times greater, which is more important in many situations 
- 802.11g
	- copes the OFDM modulation methods but operates in the narrow 2.4ghz ism band.
	- same rates as 802.11a 

### 4.4.3 the 802.11 mac sublayer protocol 
- radios are nearly half duplex, meaning that they cannot transmit and listen for noise bursts at the same time on a single frequency. 
- 802.11 tries to avoid collisions with a protocol called CSMA/CA (collision avoidance)
	- channel sensing before sending and exponential back off collisions
	- a station that has a frame to send starts with a random backoff, it doesnt wait for a collision. 
- compared to ethernet 
	- strarting backoffs early helps to avoid collisions
		- this avoidance is worthwile because collisions are expensive, as the entire frame is transmitted even if one occurs 
		- acks are used to infer collisions becasue collisions cannot be detected 
- this mode of operation is callled DCF (distributed coorindation function)
	- each station acts independently without any kind of central control 
- standard also includes an optional additional mode of operation called PCF (Point coordination function) in wich access points controls all activity in its cell, just like a celluar base station 
- PCF isnt used in practice because there is normally no way to prevent stations in another nearby network from transmitting competing traffic 
- reliability, in contrast to wired networks, wireless networks are noisy and unreliable, due to intereference from radio waves
	- the use of acks and retransmissions is of little help if the probabiltiy of getting a frame through is small in the first place 
- the main strat is to lower the transmission rate, slower rates use a more robust modulation that are more likely to be received corectly for a given signal to noise ratio. 
- if to many frames are lost a station can lower its rate
- another strat, send shorter frames, if the probability of any bit getting in error is p, the probability of an n-bit frame being received entirely correctly is $(1-p)^n$ 
- shorter frames can be implemented by reducing the max size of the message that is accepted from the network layer 
- alternatively 802.11 can split frames into smaller pieces called fragments, each with its own checksum. the fragments are numbered and acked using a stop and wait protocol (the sender may not transmit fragment k + 1 until it has been ack for k). once the channel has been acquired, multiple fragments are sent in a burst.  they go one after the other with an ack in between, until eitehr the whole frame has been sent or the transmission time reaches the max allowed 
- saving power, beacon frames, periodic broadcasts by the AP. the frames advertise the presence of the AP to the clients and carry out system paramters
- cleints can set a power-managemnt bit in frames that they send to the AP to tell it that they are entering power-save mode, client can doze and the AP will buffer traffic intended for it
	- to check for incoming traffic, the client wakes up for every beacon, and checks a traffic map that is sent as part of the beacon. 
	- another power saving mech is called APSD (automatic power save delivery)
		- the Ap buffer frames and sends them to a client just after the client sends frames to the AP
- quality of service, by extending CSMA/CA with carefully delivered internvals between frames.
	- after a frame has been sent, a certain amount of idle time s required before any station may send a frame to check that the chnalle is no longer in use. 
	- ![[Screenshot 2023-04-11 at 1.00.47 pm.png]]


### 4.4.4 802.11 frame structure 
- 3 different classes of frames 
	- data 
		- first the frame control field
		- version
			- set to 00, allow future version of 802.11 to operate at teh same time in the same cell
		- then come the type (Data, control, or management) and subtype fields (RTS,CTS)
		- the to ds and from ds bits are set to indicate whether the frame is going to or coming from the network connected to the APs, with is the distribution system 
		- the more fragments bit mean that more fragments will follow
		- retry bit marks a retransmission of a frame sent earlier 
		- power management indicates that the sender is going into power save mode
		- more data - the sender has additional frames for the receiver 
		- protected frame - the frame body has been encrypted for security
		- order bit - tells the receiver that the higher layer expects the sequnce of frame to arive stricly in order
		- ![[Screenshot 2023-04-11 at 1.05.35 pm.png]]
		- duration field 
			- how long the frame and its ack will occupy the channel, measures in ms
		- address 
			- data frames sent to or from an AP have 3 addresses
				- first reciever 
				- second the transmitter 
				- distant endpoint 
		- sequence field 
			- numbers frames so that duplicated can be detected 
			- of the 16 bits that can be used
				- 4 identify the fragment 
				- 12 carry a number that is advanced with each new transmission 
		- data field 
			- contains the payload 
			- up to 2312 bytes 
			- the first bytes of this payload are in a format known as LLC (Logical link control)
				- the glue that identifies the higher layer protocol to which the payloads should be passed 
		- frame check sequence 
			- same 32-bit crc 
	- control 
	- management 
		- they have the frame control, duration, and frame check sequence fields
		- however they may have only one address and no data portion 

### 4.4.5 services 
- association and data delivery 
	- used by mobile stations to connect themselves to APs. 
	- used just after a station moves within radio range of the AP
	- upon arrival the station learns the identiy and capabilites of the AP, either from beacon frames or by directly asking the AP. 
	- capabilites include 
		- data rates supported 
		- security arrangementes 
		- power saving capabilites 
		- quality of servce support 
	- include a SSID (service set identifier)
	- while beacons are always broadcast, the SSID may or may not be broadcasted 
	- reassocation allows a station to change its preferred AP
- security and privacy 
	- must auth before sending frames via the AP
	- with WPA2, the ap can talk to an auth server that has a username and password database to determine if the statoin is allowed to access the network 
	- another auth apporach that is commonly used in enterprise networks is 802.1X, implements port based auth
		- relies on centralised auth, which creates the possibilites for more fine grained access control, accounting billing and attribution
	- the station that is authing is called a supplicant, this device auths to the network through an auth framework called EAP (enhanced auth protocol)
- prioritisation and power control 
	- Qos traffic scheduling service 
	- uses protocols to give voice and video traffic preferential treatment compared to best effort and background traffic 
	- companion service also provides higher-layer timer synchonrisatoin 
	- allows for stations to coordinate their actions which may be useful for media processing 
	- two servcies that help stations manage their use of the spectrum 
		- transmit power control 
			- gives stations the information they need to meet regulatory limits on trasmit power that vary from region to region 
		- dynamic frequcny selection service
			- give stations the information they ned to avoid transmitting on frequnecies in the 5ghz band that are being usef for radar in the proximity

## 4.8 summary 
- some netwokrs have a single channel that is used for all communications
	- these networks have a key design issue that is the allocation of the channel among the competing stations wishing to use it 
	- FDM and TDM are simple, efficicent aloocation schemes when the number of stations is small and fixed and the traffic is continuous 
- numerious dynamic channel allocation algorithms have been devised 
	- the ALOHA protocol 
		- with and without slotting 
