
- at once we have DL_DATA and DL_ACK frames travelling in each direction 
- the small DL_ACK frames consume much bandwith, and increase the number of hardware interrupts 
- instead, we use frame piggybacking 
	- when the reciever gets a DL_DATA frame, it doesnt immediately send an DL_ACK frame 
	- the reciever waits until it has its own outgoing DL_DATA frame, and the piggybacks the pending DL_ACK in the outgoing header 
	- if no DL_DATA frame becomes available in a short time, the receiver must send an DL_ACK frmae