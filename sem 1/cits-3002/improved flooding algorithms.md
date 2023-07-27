
- disadvantage
	- flooding really does flood the network with packets 
- partial solutions
	- do not retransmit pacekts on the link on which they arrived - they have already travelled from that direction 
	- each packet can include a hop count and after any hop count exceed the diameter of the network the packet can be discarded 
	- acknowledgemnets need only be transmitted on the link on which the data packet arrived 
	- as data packets arrive, each router can remeber the link of minimum hop count on which it arrived - all subsequent packets for that destination go on that link 
	- routers can keep a list of sequence numbers seen and if any packets are re-seen by any router they are discarded 