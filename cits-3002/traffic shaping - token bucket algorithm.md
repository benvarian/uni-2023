
- the leaky bucket algorithm enforces a strict maximum traffic generation 
- its better to permit short bursts, but thereafter to constrain the traffic to some maximum 
- provides a bucket of permit tokens, before any packet may be transmitted, a token must be consumed
- tokens drip into the bucket at a fixed rate 
- if the bucket overflows with tokens they are simply discarded 
- ![[Screenshot 2023-03-29 at 12.48.49 pm.png]]
- packets are placed in an infinite queue
- packets may enter the subnet whenever a token is available, else they must wait 
- the token bucket algorithm enables a host to transmit in short bursts, effectively saviing up limimted permission to generate a burst 