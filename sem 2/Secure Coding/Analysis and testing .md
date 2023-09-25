# Highlights 
- avoiding vulnerabilities 
- automatic program analysis 
- static analysis techniques 
- dynamic analysis techniques
- fuzzing


## Avoiding vulnerabilites 
- there are things that we can do in 
	- analysis & design
	- implementation
	- testing 
	- maintenance 
- to reduce the change of vulnerabilities 

### Analysis & design
- security requirements can be developed in tandem with threat modelling 
- threat modelling asks the question -> "what could go wrong"
- helps identify threats 
- helps identify potential mitigations that we can put in place

### Implementation and testing 
- implement mitigation strategies identified earlier 
- use static and dynamic analysis techniques to help identify potential problems in our code 

#### Program Analysis 
- what is it 
	- process of using automated tools to analyse the behaviour of computer programs for particular properties 
- where is it used?
	- compiler development 
	- verification 
		- test if program is correct
	- security 
		- want to find code that can lead to vulnerabilities 

##### Program analysis approaches 
- static 
	- performed without executing the program 
	- examples 
		- flawfinder 
		- clang-tidy
- dynamic 
	- performed at runtime 
	- operate on the source code of the program
	- require the program to run in order for it to work
	- widely applied in security in the form of runtime memory error detection, fuzzing, dynamic symbolic execution and taint tracking 
	- examples 
		- valgrind 
			- simulates the effect of every instruction in the original program
			- doesn't require a re-compile, uses the original binary and inserts extra instructions
		- sanitisers 
			- Address Sanitiser (ASan) -> detects buffer overflows and other similar memory errors 
			- Thread Sanitiser (TSan) -> data races and deadlocks
			- UndefinedBehaviourSanitiser (UBSan) - detects various sorts of undefined behaviour 
- hybrid 
	- mix of two
### dynamic vs static 
-  dynamic can be very fast and precise 
	- will be very precise as to where the problems occur 
- limited to only code that was actually executed 

## Static analysis concepts 
- cannot be as precise as dynamic 
- static approximates the behaviour of the program, they provide either false positives or false negatives 
	- False positive 
		- reporting that the program has some property when its not 
	- False negative 
		- a program does not have some property when it does

### Soundness and completeness 
- Sound 
	- if the analyser asserts that a program has property P, then the program does have property P. 
	- could be wrong and lie about the presence of P
- Completeness
	- if a program has property P, then the analyser always detects it 
- compromises
	- we would like an analysis to be both sound and complete 
- phrasing 
	- what sort of error you think an analyser is making depends on how you phrase the question
	- if your analyser if looking for property P, but sometimes classifies programs as dividing by zero when they don't, then its incomplete 
	- if your analyser is looking for property $\neg P$, but sometimes classifies programs as dividing by zero when they dont, then its unsound 

### reporting security errors 
- ![[Screenshot 2023-08-26 at 3.24.16 pm.png]]

## Sorts of static analysis 
- type checking
	- prevents runtime errors
- style checking 
	- makes code easier for humans to review 
- property checking 
	- avoid some security bugs 
- program verification 
	- ensures correctness with a specification
- bug finding 

## Type systems 
- powerful type systems can provide strong guarantees about program behaviour 

## Style checking 
- style checking covers good practice 
- covers coding conventions 
- naming conventions 
- checks for dubious code constructs 


## language based security 
- use language features to check for application level attacks 
- add security labels to data inputs and data outputs 
- tainted 
	- data from unsafe source 
	- data derived from or influenced by tainted data 
- untainted 
	- data we can safely output or use

### type checking information flow 
- idea 
	- define a type system which tracks security levels of variables in the program, adding levels to sources and sinks 
- security levels can be 
	- high 
		- sensitive information -> personal details 
		- any other data that 
			- is computed directly from high data 
			- occurs in a high context 
	- low 
		- public information 


## fuzzing 
- mutation based ("dumb")
	- little to no knowledge of the structure of inputs 
	- easy to set up
	- depends on input provided
- generation based (smart)
	- test cases are generated from some description, rules or grammar 
	- harder to set up
	- knowledge of input structure usually gives better results than mutation 
- evolutionary
	- generates inputs based on the response of program 