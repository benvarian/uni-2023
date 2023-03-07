## means 
- add up all the values and divide by the number of observations 
- for the matings we have 
	- ![[Screenshot 2023-03-07 at 12.56.37 pm.png]]
- and for the petal widths 
	- ![[Screenshot 2023-03-07 at 12.57.03 pm.png]]
- in R
	- mean(elephant$Matings)
	- mean(iris$Petal.Width)

## weakness of the mean
- if the distribution is skewed then the mean is misleading 
- example
	- suppose a firm has 21 employees earning 50k per year and 4 seniors managers earning 50k per year and 4 senior managers earning 500k per year 
	- acme enterprises, whose employees earn an average of 122k per year seeks further tax breaks from the council 

## median 
- if the values are ordered, then the median is the middle value 
- for the 41 elephant mating values, the median is 2
- the middle is the 21st value-there are 20 elephants on either side 

## differing numbers of observations 
- take the middle one if there are an odd number of observations 
- ![[Screenshot 2023-03-07 at 1.01.16 pm.png]]
- take the average of the two middle ones if there an even number of observations 

## mean and median 
- ![[Screenshot 2023-03-07 at 1.02.49 pm.png]]

## symmetric or skewed 
- ![[Screenshot 2023-03-07 at 1.03.03 pm.png]]

## mean vs median 
- if the data is symmetric, then the median and mean are equal 
	- right skewed 
		- the tail of the histogram extends to the right, so the mean is greater than the median
	- left skewed 
		- the tail of the histogram extends to the left, and the mean is less than the median 

## when to use which 
- the mean is more easily influenced by outliers and so in most cases it does not really and reflect a typical value 
- in common statistical practice 
	- house prices are given as medians 
	- average weekly earnings data are medians 

## some terminology
- we need to us the mathematical terminology for summation, which uses the greek letter sigma $$\sum$$
- suppose we have the observations 
	- y1, y2 ... yn
- then the expression 
	- ![[Screenshot 2023-03-07 at 1.08.45 pm.png]]
- is the mathematical terminology for the sum y1 + y2 + yn
- the "i" variable is called the index of summation 

## mean notation 
- given observations 
	- y1, y2 ... yn
- the mean is 
	- ![[Screenshot 2023-03-07 at 1.10.01 pm.png]]
- or 
	- ![[Screenshot 2023-03-07 at 1.10.15 pm.png]]
	- 