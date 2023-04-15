temporarily delaying outoging ack packets so that it can catch a free ride on teh next outgoing data frame

go back n
- when a pacekt it sent itll include somewhere what the sequence number is and if the packet received doesnt match up to that specific sequence number itll discard that packet 
- it then restarts from that count of lost packets which is costly as the first received padket could be incorrect hence meaning the whole transmission has to start all over again. 

stop and wait 
- after sending a frame making sure to wait for the host that you sent a pacekt to to respond sending an ack packet allowing for yourself to then send the next packet. 

selective repeat 
- alsomt like go back n but allows for the trnamissoin to only have to transit the lost or damaged frames which is better as it means you dont double up on the packets that get sent 

aloha 
- after each station has sent a frame to a central computer, the central computer will then rebroadcast that pacekt to all connecing computers 

slotted aloha 
- theres specific time slots that all comptuers know, then when a packet needs to be transmitted  a computer can go into one of these slots to broadcast a packet 
- dont think it deals with collisions yet but its just accepted that itll happen 


- physical
- datalink
- network
- tranmission
- session
- presentation
- application

