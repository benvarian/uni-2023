
- expect in the trivial 2 node case, some nodes will now have more than one physical link to manage 
- when the network layer presents a packet to the data link layer, it must now indicate which physical link is involved 
- each link must have its own data link protocol, its own buffers for the senders and recievers windows and state variables such as ackexpected, nextframetosend