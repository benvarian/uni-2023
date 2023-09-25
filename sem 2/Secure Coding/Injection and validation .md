## injection 
- worst type of attacks 
- CWE describes injection as 
	- ![[Screenshot 2023-08-17 at 8.24.46 pm.png]]

- example situation 
	- ![[Screenshot 2023-08-17 at 8.29.21 pm.png]]
	
### improper neutralisation 
- must always validate your inputs, especially when they'll be passed onto a downstream component 
- special element refer to semicolons or stuff that can initialise new commands 
- neutralising means to quote or escape those special commands so that they are no longer treated as special

### downstream component 
- something that takes a already pre-processed "item" and processes it 
- database receiving sql call


### injection example 
- ![[Screenshot 2023-08-17 at 8.30.03 pm.png]]


## C - high level shell spawning 
- can use system command or popen
- popen makes a pipe through which you send input to a newly spawned process or receive output from it 

### why is system unsafe?
- invokes the system shell
- delegates to the system shell the job of 
	- parsing the commands being executed 
	- finding somewhere on users path, any executables to be invoked 

### why are exec* functions safer?
- need to specify the full path to the command being executed 
- can invoke only one command, have to break up arguments yourself
- have precise control over the environment variables the executed command can see

### system precautions 
- sanitise the environment 
- pass only a fixed string argument, with no wildcard characters 

### exec precautions 
- should close all file descriptors you don't wish to deliberately pass to the child 
- drop all privileges before calling exec stuff, as new program will have same rights 


## metadata and meta-characters 
- metadata accompanies some body of data and provides additional information about it 

### in band vs out of band 
- in band 
	- embeds metadata into the data itself 
	- length of c strings:
		- encoded using NUL character as terminator in the data stream 
- out of band representation 
	- separates metadata from data 
	- length of strings 
		- in java and c++, stored seperately outside the string 

### common meta-characters
- seperators or delimeters used to encode multiple times in one string 
- escape sequences which describe additional 
	- \\n \\t

## Environment variables 
- neglected form that someone could steal from 
- if a child is created using fork(), the child inherits parents env 

### problems with path
- defines a search path to find programs 

### pre-loading attacks on unix
- unix systems use a search path for dynamic libraries which can be defined/overwridden by variables like 
	- LD_LIBRARY_PATH
	- LD_PRELOAD


