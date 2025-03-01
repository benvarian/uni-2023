- assume the size of the senders and recievers windows have been defined as integer constants with NRBUFS and MAXSEQ
- omit the declaration of structures and variables, but note that the sender will need a number of timers (one per outstanding frame), and the receiver needs record which frames have arrived (but not yet to be sent to the layer above).
- ![[Screenshot 2023-03-16 at 12.06.33 pm.png]]
- when the layer above (application layer) provides a message for delivery, we must now buffer that message for posible future retransmission 
- as we also have a finite number of buffers in the sender, we must choke or throttle the application layer when our buffers are exhausted
- ![[Screenshot 2023-03-16 at 12.25.02 pm.png]]
- we have most work to perform when a frame arrives at the physical layer - either some DL_DATA or an DL_ACK
- we must first determine if the frame has been corrupted 
- a more complex selective protocol may incorporate DL_NACKS
- ![[Screenshot 2023-03-16 at 12.32.16 pm.png]]
- when a DL_DATA frame arrives, you msut ensure that it is within the receivers range of expected frames 
- for each frame in a sequence that have arrived successfully, we send it to the layer above 
- ![[Screenshot 2023-03-16 at 12.33.28 pm.png]]
- dont send an DL_ACK for each frame received, instead we simply acknowledgment the highest sequence number correctly reeived to date 
- this DL_ACK imples all lower sequences numbers hav been reeicved as well
