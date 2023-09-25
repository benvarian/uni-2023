## Authentication and authorisation 
- authentication 
	- confirming the identity of someone or something 
- authorisation
	- checking whether someone is permitted to take a particular action 

- auth is enforced by an access control system 
	- the assumption within the access control system is that a user has been authenticated in some way 
	- main concern is what the user can legally do 

## access control system
- collection of methods and components that determines who has access to particular system resources, and the type of access they have 
- ensures all actions on resources are within the security policy 
- supports our goals of achieving confidentiality and integrity 
- bear in mind principle of least privilege 

### issues
- needs to be efficient 
	- can have many file accesses occurring every second, so our system needs to be able to make decisions quickly 
- like them to be expressive 
	- want to express complex, high level policies about who can do what 

#### Terminology 
Object
- some resource that we want to protect 
Subject 
- entities capable of doing things 

#### Example invocations
- can alice read the file x
- can bob open a TCP socket, and listen on port 80


### Matrix model
- in order to determine who can do what, we can imagine that we have a matrix listing all objects in the system and all subjects/users 
- ![[Screenshot 2023-08-17 at 7.16.20 pm.png]]
- doesn't tell us how rights can change over time?

### Types of access control system 
Discretionary Access control (DAC)
- individual users can control access to files that they own
- owners of objects set the permissions 
- do we trust the users to get all the permissions right 
- what if a user wants to download and run programs they found online 
Mandatory Access control (MAC)
- a system controls access and individual users cant alter it
- enforced by the OS
- implies that superusers/admins dont have ultimate control
- **used to ensure not even sysadmins can tamper with the OS kernel**

### Examples 
- DAC's 
	- os enforces that the low labelled files may not alter the high label ones 
	- if you download a file off the internet, and it wants access to higher level files, the user has to approve

## Deputies 
- suppose a user wants to change password, stored in sys/passwords
- cant give every user read and write permissions to that file 
- might give particular programs the ability to take actions on behalf of particular users at a high level of privilege than the user has 

## Confused deputies 
- alice sends request to a server that got started by bob
- the server uses bobs permissions to check whether a file can be read, so alice could ask for a file, which she shouldn't be allowed to have access to 

## implementing an access control matrix 
- store by "column" (resource)
	- each object is associated with a list of users, and what rights they have 
- store by row (user)
	- each subject (user) is associated with a list of objects, and what rights the user has for it

### ACL vs capabilities 
- column leads to the idea of an access control list (ACL)
- rows leads to the idea of a capability system 

#### ACL
- store rights 
- easy to implement 
- easy to revoke rights 
- difficult to determine all rights possessed by one user 
- all popular os's use it 

#### Capabilities 
- easy to determine all rights possessed by one user 
- easy to add and remove users 
- difficult to change rights of all users to one file 

### Capability systems 
- very powerful and flexible 
- subjects might have the ability to copy capabilities so they can be given to others or perhaps only to transfer capabilities

### Unix approach
- users have a user ID, and are in one or more groups
- root user is super user, user id of 0
- user nobody can be used as a defualt user for unprivileged operations 
- when determining rights to files, use a coarse grained approach and divide all principals into 
	- user/owner
	- group owner 
	- everyone else
- uses those to determine who has rights for what file as each file has a 3x3x3 "table" that allocates rules basically 

## solutions to confused deputies 
- **confused deputies arise when a process with high privileges is fooled into letting a less-privileged principal do something they shouldnt**
- split program into two processes that communicate
- ![[Screenshot 2023-08-17 at 8.14.36 pm.png]]