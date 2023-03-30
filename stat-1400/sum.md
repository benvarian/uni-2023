
- let X and Y be random variables 
- then their sum X + Y is the random variable whose value is obtained by adding the value of X and Y
- so mentally its measuring both X and Y at the same time, then adding the values 

- example sum 
	- ![[Screenshot 2023-03-30 at 12.52.26 pm.png]]

- sample of three
	- repeat the same experiment three times, and average the results 

- out assumptions 
	- view a single experiment as observing the value of a random vairable X whose variability arises from measurement error 
	- then X has some unknown probability density function 
	- ![[Screenshot 2023-03-30 at 12.53.46 pm.png]]

- repeat the dose 
	- now take three such measurements 
	- call them X1, X2 and X3 
	- we assume they have the same but unknown pdf
	- ![[Screenshot 2023-03-30 at 12.54.25 pm.png]]

- the average 
	- now we calculae the average of the three measurements 
		- ![[Screenshot 2023-03-30 at 12.54.46 pm.png]]
	- then the $\overline{X}$ is called the sample mean 
- the sample mean 
	- ![[Screenshot 2023-03-30 at 12.55.57 pm.png]]

- sampling 
	- a triplet of measurements X1, X2, X3 can be viewed as a 
	- sample size of 3 
	- ![[Screenshot 2023-03-30 at 12.56.31 pm.png]]

![[distributions]]

- means add 
	- ![[Screenshot 2023-03-30 at 12.59.49 pm.png]]

- mean of $\overline{X}$ 
	- ![[Screenshot 2023-03-30 at 1.00.08 pm.png]]

- rules for variance 
	- ![[Screenshot 2023-03-30 at 1.00.51 pm.png]]

- additivity of variance 
	- ![[Screenshot 2023-03-30 at 1.01.24 pm.png]]


- variance of $\overline{X}$ 
	- ![[Screenshot 2023-03-30 at 1.01.47 pm.png]]

- reduced variance 
	- recall that X1, X2, and X3 each have the same mean m 
	- then $\overline{X}$ also has the mean m, but a lower variance 
	- so values of $\overline{X}$ are more likely to be close to m
	- conclusion 
		- the sample mean of a larger sample is more likely to be close to the population mean 

- rules for standard deviation 
	- ![[Screenshot 2023-03-30 at 1.03.32 pm.png]]
	- adding a constant does not change the standard deviation 
	- if X is scaled by a constant b then so is its standard deviation 

- standard deviation for $\overline{X}$
	- ![[Screenshot 2023-03-30 at 1.04.30 pm.png]]
	- so the standard deviation of the sample mean is 1/3 of the standard deviation of each Xi

- sample size of n
	- ![[Screenshot 2023-03-30 at 1.05.06 pm.png]]

- satistics of $\overline{X}$
	- sample mean is 
		- E($\overline{X}$) = m
	- the variance is 
		- var($\overline{X}$) = 1 / n * v 
	- standard distribution 
		- sd($\overline{X}$) = $1/\sqrt{n}$ x s  

- some simulation
	- pick a pdf f and a sample size n
	- repeat the following 1000 times 
		- take a sample size of n
		- find the sample mean 
	- plot the histogram of the sample means 

- example 
	- ![[Screenshot 2023-03-30 at 1.07.59 pm.png]]