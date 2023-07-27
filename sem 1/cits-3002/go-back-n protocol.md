
- requires the receiver to simply discard all frames after a bad one 
	- The _sender's window size_ corresponds to the number of frames transmitted by not yet received - it varies, grows and shrinks, over time.
	- The _receiver's window size_ corresponds to the number of frames that the receiver is willing to receive - it is always fixed, 1.
- ![[Screenshot 2023-03-16 at 11.58.31 am.png]]