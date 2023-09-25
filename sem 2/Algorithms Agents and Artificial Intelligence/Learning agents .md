---
tag: Lecture
---
## why do we want agents to learn?
- all intelligence comes from designer 
	- from the algorithm used 
	- from the heuristics used 
- has two disadvantages 
	- time consuming 
	- restricts capabilities of the agent

learning agents can
- act autonomously 
- adapt autonomously 

- note that its not true that without learning, an agent can never outperform its designer 

## model of learning agents
- performance element 
	- responsible for choosing actions that are known to offer good outcomes 
	- corresponds to the agents discussed earlier 
- learning element 
	- improving the performance element 
	- requires feedback on how well the agent is doing 
- critic element 
	- responsible for providing feedback
	- compares outcomes with some objective performance standard from outside the agent 
- problem generator 
	- responsible for generating new experience 
	- trying unknown actions which may be sub-optimal 
	- explore new actions 

### example 
- uber driver 
- performance element: you want to go into perth?, lets take x its worked well previously 
- problem generator: lets try y for a chance
- critic element: it was 5 mins quicker 
- learning element: in future go y

## learning element 
- two seperate goals 
	- wants to improve the outcome of the performance element 
	- wants to improve the time performance of the performance element 
		- how fast does it operate?
		- called speedup learning 

- design of the learning element is affected by four main issues 
	- components of the performance element to be improved 
	- representation of those components 
	- feedback available, and its source 
	- prior information available 

## performance element 
- might have many components 
	- eg
		- mapping from states to actions 
		- means to infer information from percepts 
		- information about how the world evolves
		- informations about effect of an action
- each of these components might be improved by learning 
	- eg learner
		- the driving instructor shouting brake
		- being taught to recognise an ambulance
		- learning new routes and how that effects the outcome 

### representing the performance element 
- scope of the learning element that is used to improve the performance element, will clearly depend on the representation that is used 


## feedback available 
- supervised learning (corresponds roughly to being taught by an expert)
	- agent is given a set of example input-output pairs
	- agent learns a general rule that captures these examples as special instances 
	- Class label
		- a given attribute that is put onto something 
		- can be represented as 1 and 0's 
		- generally mean a if statement basically
- reinforcement learning (corresponds roughly to learning from experience)
	- try something new and see if it works better
	- the agent experiments and remembers what worked and what didn't
- un-supervised learning (happens in the absence of feedback)
	- basically means learning patterns in the input
	- most common task is clustering 
		- partition input values into sets 
	- eg
		- taxi driver learns the difference between good days and bad days in terms of traffic
	- uses machine learning algorithms to analyse and cluster unlabelled data sets 
		- algorithms discover hidden patterns in data without the need for human intervention 
	- used for 3 main tasks 
		- Clustering 
			- grouping unlabelled data based on their similarities or differences 
		- Association 
			- uses different rules to find relationships between variables in a given dataset
			- used for market basket analysis and recommendation analysis 
		- Dimensionality reduction 
			- used when number of features in a given dataset is to high
			- reduces the number of data inputs to a manageable size while preserving data integrity


## the prior knowledge available 
- two ends of the spectrum 
	- tabula rasa 
		- agent starts with an empty state
			- only basic skills 
	- agent starts with a known good design 
		- tries to fine tune it 
- this distinction captures exploration vs exploitation 
	- do we stick with what we know (exploit), or do we try new things and hope that they work better (explore)
- most situations fall somewhere in the middle 
	- learning is hard 

## functional approximation
- all components of the performance element can be described by a function 

## inductive learning 
- in general we have to decide 
	- what mathematical operations are available for h (polynomials, exponentials, trigonometrics)
	- what trade-off we will tolerate between exactness and generalisability 
	- whether any of the data can be dismissed as outliers 


## properties of decision trees as performance elements 
- limited inputs 
	- cant take in continuous info
- limited outputs
- fully expressive wrt propositional problems
- given n attributes 
	- there will be $2^n$ combinations of inputs 
	- hence $2^{2^n}$ possible functions 

## decision trees 
- taking one part out of the other 
- taking away yes from the domains that contain no "getting rid of the junk"



## trivial induction algorithm 
- 