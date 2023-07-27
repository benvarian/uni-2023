
- althought two mobile nodes can communcate directly, the more usual approach is for all communication to be through fixed acess points 
- we say that a mobile node associates with a single access point if all of its communciations are via that point, and all such related nodes form a cell 
- communication between nodes in different cells require two access-points connected via a distribution system 
- ![[Screenshot 2023-03-28 at 7.40.10 pm.png]]
- the mechanism employed by a mobile phone node to select an access point is termed active scanning 
	1. the mobile client node sends probe frames 
	2. all access points within range reply with a probe response frame 
	3. the mobile node selects an access point and sends an assocation request frame 
	4. the access point responds with an association response frame 
- an alternative is for an access point to use passive scanning 
	- the acces point periodically sends beacon frames advertising its existence and abilites 
	- the mobile node may choose to switch to this new access point using disassociation and reassonciation frames 
- when a node selects a new access point, the new access point is expected to inform the old access point using the distribution system 