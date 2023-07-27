---
tag: Lecture
---
## information is based on three goals (CIA)
Confidentiality 
- preventing the unauthorised disclosure of information
Integrity 
- preventing the unauthorised modification of information
Availability 
- ensuring timely and reliable access to the program to users 

More goals
Authenticity 
- being confident in or able to verify the genuineness of a message or information
Accountability 
- trace back actions to entity 
Non-repudiation
- creation of evidence that an action has occurred, so a user cant say it didn't happen later

Threat 
- anything that has potential to cause harm or loss
Vulnerability 
- a flaw or weakness in a system's design, implementation or use that could be exploited to compromise security 

Attack 
- a situation where someone deliberately exploits a vulnerability and compromises security goals 
Incident 
- arises from a non-deliberate act. 
- Security incidents can still be costly and harmful


## privilege levels 
- access to certain devices, particular data or some cpu instructions may be protected by hardware 
- ![[Screenshot 2023-07-27 at 3.32.09 pm.png]]
- **a user application is normally executed at a low level of privilege, and isn't allowed to access or modify memory of other programs and memory stuff in the inner rings** 

## System Call
- the api of an operating system kernel 
- programmatic way to request a service from the kernel 
- allow code running in outer level to obtain services from one of the inner levels 

## Vulnerabilities - Buffer Overflow
