---
tag: Lecture
---
# Buffer overflows

Stack buffer overflow
- overrun a buffer declared as a variable on the stack. Attackers would rely on the fact that this would typically overwrite adjacent variables and/or program instructions 

Heap overflow 
- overrun a buffer contained in dynamically allocated memory 
- Attackers would rely on the fact that this would overwrite other data structures stored on the heap

## Mechanics of overflow 
- insert malicious code into some predictable location in memory 

## Preventing buffer overflow vulnerabilities 
- re-write in memory safe language 
- audit/static analysis 
	- tend to arise from format string vulnerabilities and common errors in managing dynamic memory 
- prevent execution of injected code 
- Address sanitizer 
	- replaces normal malloc and free functions with versions where the memory and around malloc-ed regions is poisoned 
	- reads and writes are checked to make sure they are not using addresses in the poisoned regions, if they are the program aborts
- Address Randomisation 
	- ASLR (Address Space Layout Randomisation)
		- used to prevent an attacker from reliably jumping to to some function/address in memory 
		- process 
			- start stack and heap at some random location in memory
			- map shared libraries to random locations in process memory 
- W xor X (write XOR execute)
	- provides hardware support for making segments of memory as non-executable
	- stack and heap can be put in non-executable memory
		- any fault to execute memory in those regions will result in a fault
	- marking memory as non-executable doesn't prevent data structures or return addresses from being corrupted 
- return-oriented programming
	- a return address can point to any sequence of instructions ending in a return
	- therefore it's possible to arrange the stack such that stack frames will execute a sequence of these "gadgets"

# Integer overflows and underflows
- intended wraparound of integer types in various languages 
- underflow - wraparound from the bottom 
- Exceeding the bounds of numbers representable in an integer type, resulting in undefined behaviour 
- assigning a number to a type to small to hold it, which results in a truncation

## Unsigned integer wraparound
- if you attempt to calculate a value that would go outside their bounds, the value will wrap around

## Signed integer overflow 
- exceeding the representable bounds for a type results in undefined behaviour 


# Defending against integer overflow
- use appropriate types
- do arithmetic in a wider type 
- use compiler flags 
- use libraries or code that provides safe arithmetic functions

# Compiler flags for wrap around
- ![[Screenshot 2023-08-06 at 4.42.18 pm.png]]

