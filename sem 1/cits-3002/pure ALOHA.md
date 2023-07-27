- in 1970 Norman Abramson devised the ALOHA network at the university of Hawaii
- pure aloha uses a contention based protocol 
	- users transmit whenever they wish 
	- users detect their own collisions 
	- after a collision, a users backs-off for a random time period and then retransmits 
- ![[Screenshot 2023-03-28 at 4.05.23 pm.png]]
- the expectations for throughput of this approach 
	- infinite number of users each thinking and sending 
	- generation of packets is a poisson distribution, with mean S
	- here S means the number of packets generated per packet time 
	- if S > 1, chaos 
	- is 0 < S < 1 we get acceptable throughput 
- analysis can show the best possible utilisation of 18.38%

![[slotted aloha]]
