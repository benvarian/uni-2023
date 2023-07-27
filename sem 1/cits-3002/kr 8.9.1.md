## operational security: firewalls and intrusion detection systems

### firewalls 
- allows some packets to pass and greater strengthens the network security 
- allows a network admin to controll access between outside world and reasource withim 
**- firewall has 3 goals 
	- making sure all data goes through the firewall
	- making sure the firewall itself isnt hackable 
	- only authorised traffic is allow in** 

3 types of firewalls 
- application gateway
	- acts on network layer of connection so it is able to analsye all the protocols and make decisions through the information avaialble on that layer
- traditional packet filtering 
	- simply looks at the available packet and makes decsions on the information in that packet to deem if its safe or not
- stateful 
	- tracks tcp connections from the start and if something unusual happens simply close the connection 