- each station connects to the ether with a transceiver 
- the design of the transceiver must be an exercie in paranoia 
- failures of the transceiver must not pollute the ether, power failure must not cloud the ether and disconnection must not be noticed by other stations 
- 802.3 uses five significant mechanisms to reduce the probability and cost of losing a packet 
	- carrier detection 
		- Ethernet uses the carrier sense mechanism of _phase encoding_ which guarantees that there is at least one phase transition on the ether during each bit time.
		- The Aloha scheme does not use carrier detection and subsequently suffers a higher collision frequency.
	- packet error detection 
	- interference detection 
		- each transceiver has an interference detector, a station can detect interference because what it is receiving is not what it is transmitting 
		- has 3 advantages 
			1. a station can detect collisions and re-schedule transmission 
			2. interference is detected within the propagation time (with aloha a whole packet was transmitted and then examined for a collision)
			3. the frequency of collisions is immediately used to dynamically change the back-off times 
	- truncated packet filtering 
		- interference detection and deference cause most collisions to result in truncated packets of only a few bits 
		- to reduce the overhead of obviosuly damaged packets, the hardware is able to filter them out 
	- collision consensus enforcement 
		- whenver a station detects a collision of its own transmission it deliberately jams the ether to ensure that other collding station hear the collision as quickly as possible and then stop transmitting 
