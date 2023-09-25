## sdp's
- a problem where the utility obtained by an agent depends on a sequence of decisions 
- a policy is a set of state-action rules 
	- for each state which action do i take
	- **by providing a policy it turns a utility based agent into a simple reflex agent**

## optimal policies 
- something that gives the maximum reward in a state 
- depends on many things 
- changes with each state, one could be to jump becuase x, then next could be to move to the right

## bellman equation 
- ![[Screenshot 2023-09-14 at 7.06.57 pm.png]]


## value iteration 
- idea 
	- determine the utility of each state
	- then determine the optimal action in each state, by action determination 
- to determine utility of each state
	- start with arbitrary utilities U
	- update U to make them locally consistent with Bellman 
	- repeat until U is close enough 
- a method for finding the optimal value function by solving the bellman equations iteratively 
- uses dynamic programming to maintain a value function that approximates the optimal value function 

## policy iteration operation 
- in each iteration 
	- derive the utilities from the current policy 
	- check each state to see if its actions is optimal 
	- if there are updates -> iterate again

## eternal agents
- ????