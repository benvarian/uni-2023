## topics 
- race conditions, data races, TOCTOU bugs 
- files and best practices 
- detecting and mitigating race conditions 
- data races in multithreaded programs 

## intro 
TOCTOU (Time of Check to Time of Use)
- ![[Screenshot 2023-09-25 at 12.18.47 pm.png]]
	- create a file, and after the first check is done to make sure the person can open the file, you create a link to another file that contains potentially dangerous contents 

### how to exploit 
- requires precise timing 
- attacker can potentially slow down the system to give them more time to execute attack

### terminology 
- race condition
	- when the timing or order of events affects the correctness of a piece of code 
- data race 
	- in languages which permit concurrent access to memory
	- a situation where one thread is mutating some location in memory, and the other threads that access that location produce incorrect views of the same data
- TOCTOU bug
	- a particular type of race condition where we check whether 

### data race example 
- thread A starts writing to a value 
- thread B reads like halfway through 
- thread B will get some junk value that means nothing 

## Race conditions and file handling 
Files and race conditions 
	- files and directories are very common resources that can cause race conditions 
Vulnerable to 
- symbolic linking exploits 
	- TOCTOU example
- temporary file open exploits 
- the unreliable use of filenames 
	- relying on a file name to always refer to the same file is very unreliable
	- example 
		- we have 2 files 
		- program calls stat to get information about them
		- but by the time the program access those files, the files have been swapped around 

### File paths vs inodes 
- whenever a file path is used, the kernel resolves the file path into something called the inode
	- Inode 
		- a structure in the file system that describes some data on the disk
- filenames might change, and can allow for multiple filenames to point to a single inode, but once a file path has been resolved, and the file has been opened, we know it to always refer to the same file 
- ![[Screenshot 2023-09-25 at 12.36.51 pm.png]]
- so to stop these types of vulnerabilities from occurring, we use file descriptors over a pathname 
- ![[Screenshot 2023-09-25 at 12.37.37 pm.png]]

#### File-descriptor based functions 
- ![[Screenshot 2023-09-25 at 12.38.01 pm.png]]

### Temporary file bugs 
- ![[Screenshot 2023-09-25 at 12.39.44 pm.png]]
- problem 1 
	- some uses replace the X's with the process ID plus a single letter 
	- some use random numbers for the X's 
- problem 2 
	- there is a race condition
	- in between the creation of the file, an attacker can create a file with the same name 
	- how to patch
		- use mkstemp(char \*temp)
		- gives a file descriptor

### Using temp files (best practices)
- dont reuse filenames 
- use cryptographically strong random number generators 
- delete your temp files asap
- potentially create temp files in a temp directory that only you have access to


## Detecting and mitigating race conditions 
- multiple approaches 
	- remove concurrency 
		- not always possible
		- can replace non-atomic operations with an atomic one 
	- eliminate the shared resource 
		- can we use file descriptors instead of file names?
		- can we not use shared directories?
- control access to the shared object, so that it can't be unexpectedly changed 
- detecting race conditions 
	- it is often difficult to detect and reproduce these problems, but one way you can try is through the use of static and dynamic analysis
	- use of flawfinder 
	- for data races - one of googles sanitisers is ThreadSanitiser 
		- helps detect data races 
		- slows program down and uses more memory 
		- to use the feature compile the program with -fsanitize=thread

## Data races 
- occur when two or more threads access some shared variable
	- ether at the same time 
	- at least one of the accesses is a write 
- result from assuming operations are atomic when they're not 

### Solutions 
1. locking 
	- pthreads library is frequently used for multithreaded programs 
	- provides functions for creating, locking and unlocking mutexes 
	- ![[Screenshot 2023-09-25 at 1.00.01 pm.png]]
	- for each bit of data that you want to control access to, its up the individual 
		- create a mutex that controls access to that data 
		- ensure that all code that uses the data acquires a lock on it first 
		- release the lock when finished 
	- **approach is very easy to get wrong**
- mutex example 
	- ![[Screenshot 2023-09-25 at 1.02.02 pm.png]]
	- attacker can credit account with a large sum of money, and simultaneously make many concurrent withdrawals
	- examples using C
		- ![[Screenshot 2023-09-25 at 1.03.28 pm.png]]
	- or you can use the <stdatomic.h> header in C11
		- ![[Screenshot 2023-09-25 at 1.04.01 pm.png]]
	- java 
		- uses async/await to lock things down until they are done