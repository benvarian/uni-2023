
- still a possisbility that errors on the channel cause the frames to be lost entirely 
- in particular the DLL_ACK and DLL_NACK frames themselves may be lsot and the sender will be left wating forever 
- the big question is: how long should the sender wait for an acknowledgement?
- well need to handle the concept of time in our programs and implement protocols which perform nominated actions when interesting events occur 
- sender 
	- ![[Screenshot 2023-03-15 at 1.16.32 pm.png]]
	- ![[Screenshot 2023-03-15 at 1.16.44 pm.png]]