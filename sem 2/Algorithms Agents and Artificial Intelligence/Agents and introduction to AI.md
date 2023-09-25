## acting rationally 
- act in such a way as to achieve goals, given beliefs 
- define an agent, and give it 
	- some goals 
	- ability to perceive its surroundings 
	- ability to perform actions 
	- ability to reason 


## what is an agent?
- perceives its environment through sensors 
- acts on its environment through effectors 
- ![[Screenshot 2023-08-08 at 12.38.14 pm.png]]
- perceives its environment, takes actions autonomously in order to achieve goals, and may improve its performance with learning or acquiring knowledge 
- example could be a thermostat and giving it the ability to change the temperature accordingly 

## rational agents
- tries to do the right thing with a set of goals or utilities 
- the right thing can be specified by a performance measure defining a numerical value for any environmental history 
- **rational action is whatever action maximises the expected value of the performance measure**
- rational ≠ successful 
- an agents behaviour is specified by an agent function mapping percept sequences to actions 

## simple reflex agents
- choose an action using condition-action rules
- eg if the cars break lights come on
	- apply brakes
- no history is stored
- **decisions or actions are taken based on the current percept, does not depend on the rest of the percept history** 

## mode-based reflex agents
- stores memory from past 
- understands the effects of actions 
- requires internal state
	- you see a pedestrian ahead signal to a bus -> you know the the bus is going to stop -> change lanes

## goal based agents 
- ![[Screenshot 2023-08-08 at 12.48.11 pm.png]]
- achieving goals and predicting the future 
	- if i do action x, how will it effect that world 
- requires search

### utility based agents 
- goal is a binary thing 
	- fail or pass
- most outcomes are more continuously-measured 
	- which action will make me happier or richer 
- usually defined as a utility to be maximised 
- agent should try to maximise expected utility 

## Aspects of ai

### Natural Language processing
- process of applying meaning to text
- requires a machine to understand the intent and meaning behind a sentence, which requires knowledge of the world 
- statistical approaches build statistic models of meaning by sampling large corpuses of text

### Computer vision
- based on advent of convolution neural networks and deep learning 
- images and videos are represented as high dimensional vectors, and passed through many layers of a neural network 
- **enables computers and systems to derive meaningful information from digital images, videos and other visual inputs, and take actions based upon that information**
	- **if AI enables computer to think, then computer visions enables them to see, observe and understand **
- **works very similar to humans, except humans have a history of images stored in brain so its much easier** 

### optimisation 
- building abstract simulations of the environment, and trialling different actions to see which provides the greatest utility 
- this task is mainly modelling and prediction 
	- how should the simulated environment respond to different actions 

### Argumentation and reasoning 
- process of applying logical deductions and inferences to reach a conclusion from a premise 
- done via rule based systems, where premises are transformed and match with patterns, where deductions can be extracted 
- basically knowledge rep, uses prob log and depth first searches to deduct which is the correct answer
