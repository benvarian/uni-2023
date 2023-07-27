
- with each station that wants to transmit, it has to listen to the ether and on finding it silent begins transmission 
- on detecting a collision a station:
	- backs off for a random period, this is a multiple of the 802.3 slot time 
	- after the first collision each station backs-off for 0 or 1 slot times before trying again 
	- if there is a second collision, a station backs off for 0,1,2 or 3 slot times 
	- in general, a station will back off from 0 to $2^{i-1}$ slot times after the ith collision 
	- this continues for a maximum of 10 collisions, after which the station stays at 1023 for 6 more collisions 
	- after 16 collisions the station considers the 'ether' served and reports back to the networking layer 
**- this method, termed binary exponential back off, ensures a short delay for each station when a small numer of stations collide and a reasonable delay when many stations collide** 