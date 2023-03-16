
- look at the mandatory reboot_node() function 
- the simple handler of EV_DEBUG1 which prints the runtime stateof the stopandwait protocol 
- ![[Screenshot 2023-03-16 at 11.29.48 am.png]]
- two things to note 
	- embedding a cnet function call in CHECK() provides a convenient way to check that the call succeeded 
	- the last 3 lines ensure that data traffic only flows one way, and its acknowledgments only flow th eother 
